# `server.dll`

## 1. Architectural Overview

The `server.dll` module implements a multithreaded, single-instance game server for *Europa 1400: Gold Edition*. Its core architecture revolves around a central game loop that manages player connections, processes network commands, and synchronizes game state.

### Key Components:

-   **Main Thread**: The primary thread responsible for loading the DLL, initializing the server, and spawning the main game loop.
-   **Game Loop (`srv_GameLoop`)**: A dedicated thread that runs the main server logic, including accepting clients, processing data, and managing the game simulation.
-   **Networking**: A socket-based networking layer using Winsock for client-server communication.
-   **Game State Management**: A set of functions and data structures responsible for tracking players, objects, and the overall game world.

## 2. Server Initialization and Shutdown

### Initialization (`Init` -> `srv_GameLoop` -> `srv_InitServer`)

1.  **`Init`**: The exported entry point that starts the server. It creates a new thread executing `srv_GameLoop`.
2.  **`srv_GameLoop`**:
    *   Reads server configuration from `game.ini` (e.g., port, max players).
    *   Calls `srv_InitServer` to set up the server environment.
    *   Enters the main loop to handle game logic and network traffic.
3.  **`srv_InitServer`**:
    *   Initializes error handling and memory management (`m_alloc_init`).
    *   Loads essential game data using `load_game_data`.
    *   Initializes the network sockets via `srv_InitSockets`.

### Shutdown (`Exit`)

1.  **`Exit`**: The exported function to terminate the server.
2.  It sets a global shutdown flag (`g_shutdown_flag`) to signal the `srv_GameLoop` to exit gracefully.
3.  It waits for the game loop thread to finish before cleaning up resources and terminating the thread.

## 3. Networking Layer

The server uses a standard TCP-based networking model built on the Windows Sockets API (Winsock).

### Socket Initialization (`srv_InitSockets`)

-   Creates a non-blocking TCP socket.
-   Sets socket options (`SO_RCVBUF`, `SO_SNDBUF`).
-   Binds the socket to the configured server port.
-   Listens for incoming connections with a backlog of 5.

### Client Connection (`srv_AcceptClient`)

-   Accepts new client connections using `accept`.
-   Assigns each client to an available slot in the `g_client_slots` array.
-   Initializes the client's state, including a unique ID, network buffers, and a timeout counter.
-   The first connected client is designated as the "serving host" and is granted additional privileges.

## 4. Game Logic and State

### Main Game Loop (`srv_GameLoop`)

The main loop is responsible for:

-   **Accepting new clients**.
-   **Broadcasting server status** to connected clients every 3 seconds.
-   **Processing incoming client commands** via `srv_ProcessClientCommands`.
-   **Sending queued outgoing commands** via `srv_SendQueuedCommands`.
-   **Checking for client timeouts and disconnections**.
-   **Synchronizing game state** once all players are ready.
-   **Running the main simulation tick** (`sim_UpdateCitizenAge`) when the game is active.

### Key Data Structures:

-   **`g_client_slots`**: A global array that holds the state for each connected client.
-   **`g_shutdown_flag`**: A global flag to signal the server to shut down.
-   **`g_server_port`**: The TCP port the server listens on.
-   **`g_max_players`**: The maximum number of players allowed.

## 5. Game Object Allocation

The server uses a pre-allocated memory pool to manage game objects, including buildings, rooms, and other entities. This approach avoids the overhead of dynamic memory allocation during gameplay.

### Building Allocation (`gm_AllocBuilding`)

-   Retrieves a free building slot from a global array using `gm_GetFreeBuildingSlot`.
-   Initializes the building's data, including its type, owner, and other attributes.
-   Allocates associated objects, such as rooms and inventory, using `gm_AllocRoom` and `gm_AllocObject`.

### Room Allocation (`gm_AllocRoom`)

-   Allocates a new room within a building.
-   Initializes the room's properties and creates associated objects.
-   Establishes the hierarchical relationship between the building and the room.

### Object Allocation (`gm_AllocObject`)

-   Allocates a new game object and initializes its data.
-   Assigns a parent object to establish a scene graph-like hierarchy.
-   This is the core function for creating all game entities.

## 6. Player Management

### Player Allocation (`gm_AllocPlayer`)

-   Allocates a new player from a global player data array.
-   Initializes a wide range of player attributes, including:
    -   Player type and class.
    -   Family relationships (father and mother).
    -   Skills and attributes (randomized within certain bounds).
    -   Initial state and inventory.
-   Interacts with other game systems, such as the alchemist and building systems, to set up the player's initial conditions.

### Player Data Retrieval (`handleGetPlayerById`)

-   Retrieves a player's data from the global player array using a simple linear search.

### Player Killing (`cm_KillPlayer`)

-   The `cm_KillPlayer` command handler is responsible for killing a player.
-   It calls `gm_KillSpieler` to perform the actual cleanup, which includes removing the player from the game world and updating their state to "dead".

## 7. Object Manipulation

### Moving Objects (`cmdt_MoveObject`)

-   The `cmdt_MoveObject` command handler is responsible for moving objects between containers.
-   It uses `gm_RemoveObjectNoKill` to remove the object from its source container and `gm_AddObject` to add it to its destination container.
-   This mechanism is used for a variety of in-game actions, such as moving items between a player's inventory and a building's storage.

### Selling Objects (`cmdt_SellObject`)

-   The `cmdt_SellObject` command handler is responsible for selling objects.
-   It uses `gm_RemoveObject` to remove the object from the seller's inventory and `gm_AddObject` to add it to the buyer's inventory.

## 8. Crafting and Production

### Object Production (`cmdt_ProduceObject`)

-   The `cmdt_ProduceObject` command handler is responsible for producing new objects.
-   It checks if the required resources are available in the building's inventory using `gm_GetBuildingItemCount`.
-   It verifies that the building has enough space to store the new object using `gm_IsBuildingInventoryFull`.
-   If the conditions are met, it creates the new object and adds it to the building's inventory.

## 9. Worker Management

### Worker Employment (`cm_EmployWorker`)

-   The `cm_EmployWorker` command handler is responsible for employing new workers.
-   It calls `handleCreateCitizen2` to create a new citizen (worker).
-   It then adds the new worker to the specified building.

## 10. Building Management

### Building Creation (`cm_CreateBuilding`)

-   The `cm_CreateBuilding` command handler is responsible for creating new buildings.
-   It calls `gm_AllocBuilding` to allocate and initialize the new building.

## 11. Player Economy

### Setting Player Money (`cm_SetPlayerMoney`)

-   The `cm_SetPlayerMoney` command handler is responsible for setting a player's money.
-   It retrieves the player's data by their ID and then updates their money value.

## 12. Player Social Status

### Setting Player Title (`cm_SetPlayerTitle`)

-   The `cm_SetPlayerTitle` command handler is responsible for setting a player's title.
-   It retrieves the player's data by their ID and then updates their title value.
-   It also calls `handleRemovePlayerFromAmtWithCleanup` to update the player's "Amt" information, which appears to be related to their social standing.

## 13. Player Skills

### Setting Player Skill (`cm_SetPlayerSkill`)

-   The `cm_SetPlayerSkill` command handler is responsible for setting a player's skill.
-   It retrieves the player's data by their ID and then updates their skill value.

## 14. Simulation

### Updating Citizen Age (`sim_UpdateCitizenAge`)

-   The `sim_UpdateCitizenAge` function is responsible for updating a citizen's age.
-   It takes the number of days, months, and years to add to the citizen's age and then updates the citizen's data structure accordingly.

### Setting Citizen Data (`sim_SetCitizenData`)

-   The `sim_SetCitizenData` function is responsible for setting a citizen's data.
-   It sets the gender, age, and birth year of a citizen.

## 15. Lobby Management

### Getting Player List (`lobby_get_player_list`)

-   The `lobby_get_player_list` command handler is responsible for retrieving the list of players in the lobby.
-   It iterates through the connected clients and sends a list of player IDs to the requesting client.

### Setting Player Ready Status (`lobby_set_player_ready_status`)

-   The `lobby_set_player_ready_status` command handler is responsible for setting the ready status of a player in the lobby.
-   It updates the client's state and then broadcasts the new status to all other clients in the lobby.

### Joining Game (`lobby_join_game`)

-   The `lobby_join_game` command handler is responsible for allowing a player to join the game from the lobby.
-   It checks if the game is full, and if not, it assigns the player to a slot and broadcasts the updated player list to all clients in the lobby.

This initial analysis provides a foundational understanding of the server's architecture. The next steps will involve a deeper dive into the command processing and game state management functions to map out the network protocol and game-specific logic.
