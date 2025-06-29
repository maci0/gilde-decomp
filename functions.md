# Functions

## Entry Points & Core Server

### DLL Entry Points & Exports

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `entry` | `0x1001b9d4` | 100% | High | The true entry point of the DLL. | |
| `DllMain` | `0x1001b8fb` | 100% | High | The main entry point for the DLL. | |
| `DllMain_Internal` | `0x10009310` | 100% | High | Internal DllMain function. It's a stub function that returns 1. | No analysis needed. |
| `Init` | `0x10009320` | 100% | High | Server entry point. Creates the main game loop thread. | Exported function. |
| `Exit` | `0x10009350` | 100% | High | Server exit point. Terminates the game loop thread. | Exported function. |

### Main Loop & Initialization

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `srv_GameLoop` | `0x100093a0` | 90% | High | The main server loop. After calling `srv_InitServer`, it enters a `while` loop controlled by `g_bShutdownFlag`. In each iteration, it calls `srv_AcceptClient`, `srv_ProcessClientCommands`, and `srv_LoadGameState`. It yields execution with `Sleep(1)`. | Core of the server logic. Handles the entire game lifecycle from initialization to shutdown. |
| `srv_InitServer` | `0x10009d30` | 100% | High | Initializes the server's core components. It sets the thread priority, initializes the custom memory allocator (`m_alloc_init`), loads game data (`aemter_LoadFromFile`), and initializes network sockets (`srv_InitSockets`). | This is a critical function called once at the beginning of the `srv_GameLoop`. It orchestrates the entire server setup. |

## Networking

### Socket Management

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `srv_InitSockets` | `0x10009e60` | 100% | High | Initializes the server's network sockets using Winsock. It follows the standard sequence: `WSAStartup`, `socket`, `setsockopt` (SO_REUSEADDR, SO_RCVBUF, SO_SNDBUF), `bind`, and `listen`. | A core networking function that prepares the server to accept client connections. |
| `srv_AcceptClient` | `0x1000a080` | 90% | High | Accepts new client connections non-blockingly using `select`. If a connection is pending, it calls `accept` and assigns the new client to a free slot. | Handles the initial client handshake efficiently without blocking the main loop. |
| `srv_CloseClientConnection` | `0x1000a2e0` | 95% | High | Closes a client connection and cleans up associated resources. | Renamed from `close_connection`. |
| `srv_Cleanup` | `0x1000a010` | 95% | High | Cleans up all active sockets and associated resources. This includes shutting down and closing individual client sockets, the main server socket, and performing general memory and error handler cleanup. | Renamed from `sockets_cleanup`. |
| `srv_HandleWinsockError` | `0x1000ad40` | 95% | High | Handles Winsock errors by logging a descriptive message based on the error code. | Renamed from `handle_winsock_error`. |

### Data Transmission

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `srv_SendData` | `0x1000a490` | 95% | High | Sends data to a client connection. It handles partial sends, timeouts, and Winsock errors. | Renamed from `send_data`. |
| `srv_RecvFromClient` | `0x1000a340` | 95% | High | Receives data from a client connection using a non-blocking `select`. It reads the command header to determine the message size and then reads the full message. | Handles timeouts and Winsock errors gracefully. Appears to handle message framing. |
| `send_broadcast_message` | `0x10001130` | 95% | High | Sends a UDP broadcast message to `255.255.255.255` for server discovery on the local network. It creates a UDP socket and sets the `SO_BROADCAST` option. | Standard implementation for LAN server discovery. |

### Command Handling

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `srv_ProcessClientCommands` | `0x1000a570` | 85% | High | Processes incoming commands from all connected clients. It iterates through the client list, calls `srv_RecvFromClient` to read data, and then dispatches the received commands using `srv_DispatchGameCommand`. | Manages the flow of all incoming client data. |
| `srv_DispatchGameCommand` | `0x1000aac0` | 90% | High | Dispatches game commands to their appropriate handlers using a large jump table (switch statement). It reads a command ID from the client's stream and calls the corresponding `cm_*` function. | The central command router for the server. |
| `srv_HandlePlayerCommand` | `0x10010390` | 85% | Medium | A secondary command dispatcher specifically for player-related commands. It takes a subcommand ID and calls the appropriate handler. | Focuses on player-specific actions. |
| `enqueue_client_command` | `0x1000a8f0` | 95% | High | Queues a command to be sent to a client. It manages the outgoing command buffer. | Renamed variables for clarity. |
| `client_queue_append_command` | `0x1000a9a0` | 95% | High | Queues a command to be sent to a client. This function adds a command to a client's outgoing queue, but it does not send it. | Renamed variables for clarity. |
| `dequeue_command` | `0x1000aa50` | 95% | High | Dequeues a command from a client's incoming queue. It manages the incoming command buffer. | Renamed variables for clarity. |
| `srv_SendQueuedCommands` | `0x1000a860` | 95% | High | Sends pending commands to connected clients. This function iterates through active connections, sends data, and dequeues commands after successful transmission. | Renamed from `send_commands`. |
| `handle_invalid_command` | `0x1000d2e0` | 100% | High | Handles invalid or unknown commands by logging an error message. | A simple error handling function. |

## Game Logic

### Game State

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `srv_LoadGameState` | `0x10014260` | 70% | Medium | Receives and loads the complete game state from a client (likely the host). It reads a large, complex data structure containing all game objects and then calls `ls_ID2Ptr` to resolve pointers. This function orchestrates the loading of the entire game state from a file by calling various `handleLoad...Data` functions. | A critical, complex function for game state synchronization. |
| `ls_ID2Ptr` | `0x10014070` | 75% | Medium | Converts object IDs to direct memory pointers after loading the game state. This is a critical step for resolving references between all game objects. It iterates through various data structures and uses `handleGetPlayerById` and `gm_LoadGameData` to resolve the pointers. | A complex function that is not yet fully understood. |
| `handleLoadPlayerData` | `0x100142b0` | 80% | Medium | Loads player data from the game state file. This function handles different save game versions, as indicated by the numerous conditional blocks based on the value of `DAT_1002d4ec` (likely the save game version). | Called by `srv_LoadGameState`. |
| `handleLoadBuildingData` | `0x100143e0` | 80% | Medium | Loads building data from the game state file. It reads a count of buildings, and then iterates that many times, reading a fixed-size structure for each building. This suggests that the building data is stored in an array-like format. | Called by `srv_LoadGameState`. |
| `handleLoadGameData` | `0x100144a0` | 80% | Medium | Loads general game data from the game state file. This is a very large and complex function that handles the loading of many different types of game data. It contains a great deal of conditional logic based on the save game version (`DAT_1002d4ec`), and it also has special handling for different object types. The function begins by reading a count of objects, and then enters a loop to process each one. The first object type checked for is ``, which appears to be a large, complex data structure that is read in smaller chunks. The next object types checked for are `H`, `I`, and `J`, which are related to graveyards. The handling of these objects changed in save game version `0x10047`. The next object types checked for are `K`, `L`, and `M`, which are related to alchemists. The handling of these objects changed in save game version `0x10049`. This function requires further analysis to be fully understood. | Called by `srv_LoadGameState`. |
| `handleLoadGraveyardData` | `0x10012d00` | 80% | Medium | Loads graveyard data from the game state file. | Called by `handleLoadGameData`. |
| `load_alchemist_data` | `0x10012e00` | 80% | Medium | Loads alchemist data from the game state file. | Called by `handleLoadGameData`. |
| `handleLoadDynastyData` | `0x10014540` | 80% | Medium | Loads dynasty data from the game state file. | Called by `srv_LoadGameState`. |
| `handleLoadAlchemistData` | `0x10014580` | 80% | Medium | Loads alchemist data from the game state file. | Called by `srv_LoadGameState`. |
| `handleLoadTownData` | `0x100145c0` | 80% | Medium | Loads town data from the game state file. | Called by `srv_LoadGameState`. |

### Lobby

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `lobby_get_player_list` | `0x100145e0` | 95% | High | Retrieves the list of players in the lobby and sends it to the requesting client. | Renamed variables for clarity. |
| `lobby_set_player_ready_status` | `0x100146c0` | 95% | High | Sets the ready status of a player in the lobby and broadcasts the new status to all clients. | Renamed variables for clarity. |
| `lobby_join_game` | `0x100147b0` | 90% | High | Allows a player to join the game from the lobby. It assigns the player to a slot and broadcasts the updated player list. | Renamed variables for clarity. |
| `lobby_update_player_status` | `0x10014a50` | 95% | High | Updates the status of a player in the lobby and broadcasts the new status to all clients. | Renamed variables for clarity. |

### Simulation

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `sim_UpdateCitizenAge` | `0x100155c0` | 95% | High | Updates a citizen's age. It adds days, months, and years to a citizen's age. | Renamed variables for clarity. |
| `sim_SetCitizenData` | `0x10015690` | 100% | High | Sets a citizen's data. It sets the gender, age, and birth year of a citizen. | A simple and direct data modification. |

### Game Mechanics (`gm_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `gm_AllocAlchemist` | `0x1000c600` | 95% | High | Allocates and initializes a new alchemist, which appears to be a specialized type of player character. | Renamed from `alloc_alchemist`. Called from `gm_AllocPlayer`. |
| `building_SellItemTo` | `0x10019ed0` | 95% | High | Handles a player selling an item to an AI-controlled building. It checks for various conditions like building type, item category, and inventory space before adding the item. | Renamed from `add_item_to_building_inventory`. Called from `cm_ExSellObjekt` and `cm_ChkSellObjekt`. |
| `gm_AllocBuilding` | `0x100174d0` | 85% | Medium | Allocates and initializes a new building. It uses `gm_GetFreeBuildingSlot` to find an empty slot in the building data pool. | Renamed variables for clarity. |
| `gm_GetFreeBuildingSlot` | `0x10017210` | 100% | High | Retrieves a free building slot from the building data pool. It performs a simple linear search. | A straightforward and efficient implementation. |
| `gm_AllocRoom` | `0x10017c40` | 85% | Medium | Allocates and initializes a new room within a building. It also creates associated objects for the room. | Renamed variables for clarity. |
| `gm_AllocObject` | `0x10016760` | 85% | Medium | Allocates and initializes a new game object. This is the core function for creating all game entities. | Renamed variables for clarity. |
| `gm_AllocPlayer` | `0x10018850` | 80% | Medium | Allocates and initializes a new player. It manages the player data pool and initializes all of a player's attributes. | A large and complex function. |
| `gm_RemoveObjectNoKill` | `0x10016ea0` | 95% | High | Removes an object from a list without deallocating it. This is used for moving objects between containers. | Renamed variables for clarity. |
| `gm_AddObject` | `0x10016cd0` | 95% | High | Adds an object to a list, or updates its count if it already exists. This is used for moving objects between containers. | Renamed variables for clarity. |
| `gm_RemoveObject` | `0x10016de0` | 95% | High | Removes an object from a list. This is used for selling or destroying objects. | Renamed variables for clarity. |
| `gm_GetBuildingItemCount` | `0x10019cd0` | 100% | High | Retrieves the item count of a building. It has special handling for certain item types. | A simple and direct data retrieval function. |
| `gm_IsBuildingInventoryFull` | `0x10019d30` | 90% | High | Checks if a building's inventory is full. This prevents players from exceeding storage capacity. | Renamed variables for clarity. |
| `gm_KillSpieler` | `0x10017fb0` | 85% | Medium | Kills a player and performs all necessary cleanup. This removes the player from the game world. | Renamed variables for clarity. |
| `update_player_building` | `0x1000c380` | 95% | High | Updates a player's building information. | |
| `update_player_desire` | `0x1000c3c0` | 95% | High | Updates a player's desire level. | |

### Command Handlers (`cm_`, `cm_Ex`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `cm_ExAllocGebaeude` | `0x1000d350` | 95% | High | Command handler for allocating a new building. It's a simple wrapper around `gm_AllocBuilding`. | Renamed variables for clarity. |
| `cm_ExAllocSpieler` | `0x1000d460` | 95% | High | Command handler for allocating a new player. It's a simple wrapper around `gm_AllocPlayer`. | Renamed variables for clarity. |
| `cm_ExMoveObject` | `0x1000d8a0` | 90% | High | Command handler for moving an object between two containers. It calls `gm_RemoveObjectNoKill` and `gm_AddObject`. | Renamed variables for clarity. |
| `cm_ExSellObject` | `0x1000d7f0` | 90% | High | Command handler for selling an object. It calls `gm_RemoveObject` and `gm_AddObject`. | Renamed variables for clarity. |
| `cm_ExProdObjekt` | `0x1000e140` | 85% | Medium | Command handler for producing an object. It contains complex logic for handling the crafting and production system. | Requires further analysis to fully understand the production logic. |
| `cm_KillPlayer` | `0x1000f030` | 95% | High | Command handler for killing a player. It's a simple wrapper around `gm_KillSpieler`. | Renamed variables for clarity. |
| `cm_EmployWorker` | `0x1000f730` | 85% | Medium | Command handler for employing a worker. It calls `handleCreateCitizen2` to create a new worker. | Renamed variables for clarity. |
| `cm_CreateBuilding` | `0x1000fb30` | 95% | High | Command handler for creating a building. It's a simple wrapper around `gm_AllocBuilding`. | Renamed variables for clarity. |
| `cm_SetPlayerMoney` | `0x1000ffc0` | 100% | High | Sets a player's money. It directly-updates the player's money value in the player data structure. | A simple and direct data modification. |
| `cm_SetPlayerTitle` | `0x10010010` | 100% | High | Sets a player's title. It directly updates the player's title and Amt information in the player data structure. | A simple and direct data modification. |
| `cm_SetPlayerSkill` | `0x100100a0` | 100% | High | Sets a player's skill. It directly updates the player's skill value in the player data structure. | A simple and direct data modification. |
| `cm_StartCutscene` | `0x1000ff60` | 90% | High | Command handler for starting a cutscene. It calls `cm_IsCutsceneReady` and sets player flags. | Renamed variables for clarity. |
| `cm_ZombieCommand` | `0x10010260` | 95% | High | Command handler for zombie-related commands. It acts as a dispatcher, calling sub-handlers based on a command ID. | Part of the "Zombie & Graveyard" system. |
| `cm_AllocGraveyardWorker` | `0x10010310` | 95% | High | Command handler for allocating a graveyard worker. It calls `handleAllocGraveyardWorker2`. | Part of the "Zombie & Graveyard" system. |
| `cm_GetPlayerAmtId` | `0x10010350` | 95% | High | Command handler for getting a player's "Amt" ID. It calls `handleGetPlayerAmtId`. | "Amt" likely refers to an office or rank. |
| `cm_ExGetBuildingDataSize` | `0x100104a0` | 100% | High | Command handler for getting the size of a building's data. It returns the size of a building's data structure. | Used for data synchronization. |
| `cm_ExValidateBuildingData` | `0x10010530` | 100% | High | Command handler for validating a building's data. It validates specific fields within a building's data structure. | Used for data integrity checks. |
| `cm_ExGetBuildingDataPtr` | `0x100105b0` | 100% | High | Command handler for getting a pointer to a building's data. It returns a pointer to the requested data. | Used for direct data access. |
| `cm_ExIterateBuildingData` | `0x10010710` | 90% | High | Command handler for iterating over a building's data. It iterates through building data and calls a callback function. | Used for data processing and synchronization. |
| `cm_ExAllocGraveyard` | `0x10010850` | 85% | Medium | Command handler for allocating a graveyard. It allocates and initializes a graveyard building. | Part of the "Zombie & Graveyard" system. |
| `cm_ExAllocGraveyardField` | `0x100109d0` | 85% | Medium | Command handler for allocating a graveyard field. It allocates and initializes a graveyard field within a building. | Part of the "Zombie & Graveyard" system. |
| `cm_ExChangePlayerIdentity` | `0x1000d6e0` | 95% | High | Command handler for changing a player's identity. It's a simple wrapper around `gm_ChangePlayerIdentity`. | Renamed variables for clarity. |
| `cm_ExFree` | `0x1000d730` | 90% | High | Command handler for freeing a player or building. It calls `gm_KillSpieler` or `gm_FreeBuilding`. | Renamed variables for clarity. |
| `cm_ExSellObjekt` | `0x1000d930` | 80% | Medium | Command handler for selling an object with extended functionality. It contains complex logic for handling various sale scenarios. | Requires further analysis to fully understand all sale types. |
| `cm_ExClearLagerslot` | `0x1000e690` | 90% | High | Command handler for clearing a storage slot. It calls `handleRemoveObjectFromList`. | Renamed variables for clarity. |
| `cm_ExChangeDesire` | `0x1000e9c0` | 90% | High | Command handler for changing a player's desire. It updates and clamps desire values. | Renamed variables for clarity. |
| `cm_ExchangeBits` | `0x1000eaa0` | 95% | High | Command handler for exchanging bits between players. It updates player data based on size and offset. | Used for low-level data synchronization. |
| `cm_ExchangeFloat` | `0x1000eb70` | 95% | High | Command handler for exchanging a float value between players. It updates player data at a given offset. | Used for low-level data synchronization. |
| `cm_AllocCharacter` | `0x1000f980` | 95% | High | Command handler for allocating a new character. It's a simple wrapper around `gm_AllocPlayer`. | Renamed variables for clarity. |
| `cm_CanBuyItem` | `0x1000d060` | 90% | High | Checks if an item can be purchased. It handles special item types and prevents duplicate purchases. | Renamed variables for clarity. |
| `cm_ValidateLobbyAction` | `0x1000d110` | 85% | Medium | Validates lobby actions like joining and leaving. It uses a 4-byte identifier to determine the action. The return logic is inverted. | Renamed variables for clarity. |
| `cm_IsCutsceneReady` | `0x1000d260` | 90% | High | Checks if a cutscene is ready to be played. It iterates through players and checks their status. | Renamed variables for clarity. |
| `cm_Stub` | `0x1000d330` | 100% | High | Stub function that does nothing. It's a placeholder for an unimplemented command. | No analysis needed. |
| `cm_NotYetImplemented` | `0x1000d340` | 100% | High | Stub function that does nothing. It's a placeholder for an unimplemented command. | No analysis needed. |
| `cm_ExAllocObject` | `0x1000e750` | 95% | High | Command handler for allocating a new object. It's a simple wrapper around `gm_AllocObject`. | Renamed variables for clarity. |
| `cm_ExSetAttribute` | `0x1000e8d0` | 90% | High | Command handler for setting an attribute on a game object. It can be used to modify a wide range of game data. | A powerful and flexible command. |
| `cm_AdjustRelationship` | `0x1000ec00` | 75% | Medium | Adjusts the relationship between two players. It contains complex logic with different calculations based on the adjustment type. | Requires further analysis to fully understand the relationship mechanics. |

### Game Logic Handlers (`handle`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `handleGetPlayerById` | `0x100184a0` | 100% | High | Retrieves a player's data by their ID using a simple linear search. | Renamed variables for clarity. |
| `handleGetPlayerClass` | `0x10018200` | 100% | High | Retrieves the class of a player based on their type. It uses a switch statement to map the player type to a class. | Renamed variables for clarity. |
| `handleGetRandomPlayerAttribute` | `0x10018450` | 100% | High | Generates a random player attribute based on a base value. This is used for character creation. | Renamed variables for clarity. |
| `handleCreateCitizen2` | `0x10015500` | 90% | High | Creates a new citizen with specified properties. It is used by `cm_EmployWorker` to create new workers. | Renamed variables for clarity. |

### Office/Rank (`amt_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `aemter_LoadFromFile` | `0x1000baf0` | 95% | High | Loads office (Amt) data from a file. | Renamed from `amt_fio_LoadAemter`. |
| `aemter_init` | `0x1000b040` | 95% | High | Initializes the 'Aemter' (offices/ranks) data structures. | Renamed from `init_offices`. |
| `is_amt_valid` | `0x1000d020` | 100% | High | Checks if an 'Amt' (office/rank) is valid. It's a simple wrapper for `validate_amt`. | Renamed variables for clarity. |
| `validate_amt` | `0x1000b1c0` | 75% | Medium | Validates an 'Amt' (office/rank) entry based on various criteria. | Renamed from `FUN_1000b1c0`. |
| `is_amt_action_valid` | `0x1000d040` | 100% | High | Checks if an 'Amt' (office/rank) action is valid. It's a simple wrapper for `handleValidateAmtAction`. | Renamed variables for clarity. |
| `handleValidateAmtAction` | `0x1000b440` | 75% | Medium | Validates an 'Amt' (office/rank) action. It contains complex logic involving multiple global data structures. | Requires further analysis to fully understand the validation logic. |

## Low-Level Subsystems

### Memory Management

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `m_alloc` | `0x10006580` | 75% | Medium | Custom memory allocation function. It tracks memory usage with tags and statistics, and it includes checks for common memory errors. | Renamed variables for clarity. |
| `m_free` | `0x10006820` | 90% | High | Custom memory deallocation function. It includes checks for double-free and memory underflow errors. | Renamed variables for clarity. |
| `m_alloc_init` | `0x100068e0` | 95% | High | Initializes the custom memory allocator. It allocates the tracking table and initializes statistics. | Renamed variables for clarity. |
| `m_alloc_dump` | `0x10006990` | 85% | Medium | Dumps memory allocation statistics to the log. It can be filtered by tag for targeted debugging. | A useful debugging tool. |
| `m_alloc_cleanup` | `0x10006c00` | 95% | High | Cleans up the custom memory allocator. It frees all tracked memory and reports leaks. | Renamed variables for clarity. |
| `m_pool_alloc` | `0x10006d20` | 85% | Medium | Allocates memory from a memory pool. This is an efficient way to allocate fixed-size objects. | Renamed variables for clarity. |
| `m_pool_free` | `0x10006e30` | 90% | High | Frees a block of memory from a memory pool. It includes checks for invalid free attempts. | Renamed variables for clarity. |

### File System & VFS

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `file_close` | `0x10008a50` | 95% | High | Closes a file and frees its associated memory. It also calls `vfs_close_and_free` if a certain flag is set. | Renamed variables for clarity. |
| `file_read` | `0x10008a90` | 80% | Medium | Reads data from a file, handling both compressed and uncompressed data. It manages buffers, CRC32 checks, and zlib inflation. | A complex function that is central to file I/O. |
| `vfs_close_and_free` | `0x10008c80` | 95% | High | Closes a file and frees its associated memory, including the zlib inflate stream. This is used for compressed files. | Renamed from `file_close_and_free`. |
| `vfs_read_data` | `0x10008d10` | 75% | Medium | High-level function for reading data from files. It handles different file types and compression, and it performs cleanup. | Renamed from `file_read_data`. |
| `vfs_read` | `0x10008e40` | 75% | Medium | Reads data from a virtual file system (VFS) entry. It handles different file types and compression. | Renamed variables for clarity. |
| `vfs_open` | `0x10009020` | 80% | Medium | Opens a virtual file system (VFS) entry for reading or writing. It supports compressed and uncompressed data. | The entry point for all VFS operations. |

### Error Handling & Logging

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `logEvent` | `0x10002640` | 95% | High | Logs a message to a file, debug output, and/or console. This is a game-specific utility function. | Renamed variables for clarity. |
| `unhandledExceptionHandler` | `0x10002770` | 80% | Medium | Unhandled exception filter that generates a crash dump. This is critical for server stability and debugging. | A complex but important function. |
| `writeArchiveFile` | `0x10002fc0` | 98% | High | Writes data to an archive file, likely for crash dumps. This is part of the error handling and debugging system. | Comments added and improved. Global data renamed. Variable renaming partially successful. |
| `getDataBlock` | `0x10003140` | 90% | High | Retrieves a data block from a data structure. This is used by the crash dump generation system. | Renamed variables for clarity. |
| `checkMemoryProtection` | `0x10003170` | 90% | High | Checks the memory protection of a given address. This is used by the crash dump generation system. | Renamed variables for clarity. |
| `analyzeBytePattern` | `0x10003260` | 95% | High | Analyzes a byte pattern for common x86 function prologues. | Used by the crash dump generation system to improve stack traces. |
| `errorHandlerInit` | `0x10003320` | 95% | High | Initializes the error handling for the application. It sets up the unhandled exception filter and logging. | Renamed variables for clarity. |
| `errorHandlerCleanup` | `0x100034c0` | 95% | High | Cleans up the error handling system. It logs a final message and frees the console if allocated. | Renamed variables for clarity. |
| `CRT_fatal_error` | `0x10003520` | 95% | High | Handles fatal errors. It logs the error, displays a message box, and can terminate the program. | Renamed from `fatalError`. |
| `showMessage` | `0x100035c0` | 100% | High | Displays a message to the user. It can log to a file or display a message box. | A simple and direct utility function. |
| `logMessage` | `0x10003640` | 100% | High | Logs a message with file and line number information. This is valuable for debugging. | A simple and direct utility function. |
| `save_exception_context` | `0x1001e7ba` | 100% | High | Saves the exception context (exception record, context record, and EBP) to global variables for later use, likely by a crash handler. | Comments added. Variables renamed. |
| `show_message_box` | `0x10022107` | 100% | High | Displays a message box by dynamically loading the MessageBoxA function from user32.dll. | Comments added. Variables renamed. |

### Bitwise Operations

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `bitwise_select` | `0x10021298` | 100% | High | Performs a bitwise SELECT operation. | Renamed from `bitwise_op`. |
| `bitwise_select_masked` | `0x100212cd` | 100% | High | A wrapper around `bitwise_select` that clears the 19th bit of the mask. | Renamed from `bitwise_op_2`. |
| `bitwise_permute` | `0x100212e3` | 100% | High | Performs a complex bit permutation, remapping bits from the input value to different positions in the output value. | Renamed from `bitwise_op_3`. |
| `bitwise_inverse_permute` | `0x10021375` | 100% | High | Performs the inverse operation of `bitwise_permute`, restoring the original bitfield from a permuted value. | Renamed from `bitwise_op_4`. |
| `bitwise_is_range_clear` | `0x10021538` | 100% | High | Checks if a range of bits in a bitfield is clear (all zeros). | Renamed from `bitwise_op_5`. |
| `bitwise_set_and_propagate` | `0x10021581` | 100% | High | Sets a bit in the bitfield and then propagates a carry/borrow to the left. | Renamed from `bitwise_op_6`. |
| `bitwise_clear_range_and_propagate` | `0x100215d7` | 100% | High | Clears a range of bits and potentially sets a bit and propagates a carry. | Renamed from `bitwise_op_7`. |
| `bitwise_add_with_carry` | `0x100223bd` | 100% | High | Adds two unsigned integers and returns the carry bit. | Renamed from `bitwise_op_15`. |
| `bitwise_shift_left_96` | `0x1002243c` | 100% | High | Performs a 96-bit left shift on a 3-element array of 32-bit integers. | Renamed from `bitwise_op_16`. |
| `bitwise_shift_right_96` | `0x1002246a` | 100% | High | Performs a 96-bit right shift on a 3-element array of 32-bit integers. | Renamed from `bitwise_op_17`. |

## Statically Linked Libraries

### MSVC6 C Runtime (CRT)

#### Memory Management

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `CRT__heap_alloc_base` | `0x1001a835` | 100% | High | Allocates a block of memory from the heap. The allocation strategy is determined by the global variable `__active_heap`. This function is a direct implementation of `_heap_alloc_base` from the MSVC6 CRT. | MSVC6 CRT. Found in `MSVC600/VC98/CRT/SRC/MALLOC.C`, line 140. |
| `CRT__calloc_base` | `0x1001ff84` | 100% | High | Allocates a block of memory for an array of num elements of size bytes each and initializes all bytes in the block to 0. This function is a direct implementation of `_calloc_base` from the MSVC6 CRT. | MSVC6 CRT. Found in `MSVC600/VC98/CRT/SRC/CALLOC.C`, line 52. |
| `CRT_unlock_heap` | `0x1001a89c` | 100% | High | Unlocks a resource, likely the heap, using `CRT__unlock(9)`. | MSVC6 CRT. Renamed from `malloc_internal_2`. All `CRT_unlock_heap` variants are identical. |
| `CRT__unlock` | `0x1001d097` | 100% | High | Unlocks a global C runtime resource using a critical section. | MSVC6 CRT. Found in `MSVC600/VC98/CRT/SRC/MTDLL.C`, line 229. |
| `stack_unwind_helper` | `0x1001ac70` | 70% | Medium | Appears to be a helper function for stack unwinding or exception handling. | Renamed from `memory_management_3`. |
| `CRT_memmove` | `0x1001b200` | 100% | High | An optimized `memmove` implementation that handles overlapping memory regions. | MSVC6 CRT. Renamed from `memcpy_internal`. |
| `CRT_memmove_1` | `0x1001eab0` | 100% | High | An identical copy of `CRT_memmove`. | MSVC6 CRT. Renamed from `memcpy_internal_6`. |
| `memcpy_12_bytes` | `0x10021663` | 100% | High | A specialized function that copies exactly 12 bytes. | Renamed from `memcpy_internal_13`. |
| `bitstream_copy` | `0x100216a5` | 90% | High | A function that copies a stream of bits from a source to a destination, handling bit offsets. | Renamed from `memcpy_internal_14`. |
| `memset_12_bytes_zero` | `0x1002167e` | 100% | High | A specialized function that sets 12 bytes of memory to zero. | Renamed from `memset_internal_2`. |
| `CRT__heap_init` | `0x1001d3c8` | 95% | High | Initializes the C runtime heap. | MSVC6 CRT |
| `CRT__heap_term` | `0x1001d425` | 95% | High | Deinitializes the C runtime heap. | MSVC6 CRT |
| `CRT_realloc_internal` | `0x1001b5cc` | 80% | Medium | Reallocates a block of memory to a new size. It supports different heap allocation strategies, including standard heap, virtual heap, and custom heap blocks. | MSVC6 CRT |

#### String Manipulation

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `CRT_strchr` | `0x1001af30` | 100% | High | Finds the first occurrence of a character in a string. | MSVC6 CRT. Highly optimized implementation. |
| `CRT_strcmp` | `0x10021ac0` | 100% | High | Compares two strings. | MSVC6 CRT. Highly optimized implementation. |
| `CRT_strlen` | `0x1001bdd0` | 100% | High | Calculates the length of a string. | MSVC6 CRT. Highly optimized implementation. |
| `CRT_strncmp` | `0x10021200` | 100% | High | Compares a specified number of characters of two strings. | MSVC6 CRT. |
| `CRT_strncpy` | `0x1001ae20` | 100% | High | Copies a specified number of characters from one string to another. | MSVC6 CRT. Highly optimized implementation. |
| `CRT_strrchr` | `0x1001a540` | 100% | High | Finds the last occurrence of a character in a string. This function is a direct implementation of `strrchr` from the MSVC6 CRT. | MSVC6 CRT. Prototype found in `MSVC600/VC98/Include/STRING.H`, line 140. |
| `CRT_strstr` | `0x1001aff0` | 100% | High | Finds the first occurrence of a substring in a string. | MSVC6 CRT. Highly optimized implementation. |
| `CRT_strnlen` | `0x1002350a` | 100% | High | Calculates the length of a string up to a specified maximum number of characters. | MSVC6 CRT |
| `CRT__strchr_l` | `0x1002377b` | 95% | High | Finds the first occurrence of a character in a string using the specified locale. | MSVC6 CRT |
| `CRT__strdup` | `0x10023812` | 95% | High | Duplicates a string. | MSVC6 CRT |
| `CRT_strcat` | `0x1001f8e0` | 100% | High | Appends one string to another. | MSVC6 CRT |
| `CRT_strcpy` | `0x1001f60c` | 100% | High | Copies one string to another. | MSVC6 CRT |
| `str_tokenize` | `0x10021b50` | 100% | High | Tokenizes a string, similar to the standard C library function strtok. | Comments added. Variable renaming partially successful. |
| `str_tokenize_2` | `0x10021b90` | 100% | High | Tokenizes a string, similar to the standard C library function strtok, and returns a pointer to the beginning of the token. | Comments added. Variable renaming partially successful. |
| `strcpy_internal_2` | `0x1001f8d0` | 100% | High | An optimized implementation of strcpy that copies a string in 4-byte chunks. | Comments added. Variable renaming partially successful. |

#### Character Operations

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `CRT_toupper` | `0x1001b0c0` | 90% | High | Converts a character to uppercase. Wrapper for `CRT__toupper_l`. | MSVC6 CRT. Uses `CRT_pctype` and `CRT_locale_handle`. |
| `CRT__toupper_l` | `0x1001b12f` | 85% | Medium | Converts a character to uppercase using the specified locale. | MSVC6 CRT. Uses `CRT_pctype` and `CRT_locale_handle`. |
| `CRT_tolower` | `0x100213fe` | 90% | High | Converts a character to lowercase. Wrapper for `CRT__tolower_l`. | MSVC6 CRT. Uses `CRT_pctype` and `CRT_locale_handle`. |
| `CRT__tolower_l` | `0x1002146d` | 85% | Medium | Converts a character to lowercase using the specified locale. | MSVC6 CRT. Uses `CRT_pctype` and `CRT_locale_handle`. |
| `CRT_wctomb` | `0x1002075f` | 90% | High | Converts a wide character to a multibyte character. Wrapper for `CRT__wctomb_l`. | MSVC6 CRT. Uses `CRT_mb_cur_max`. |
| `CRT__wctomb_l` | `0x100207b8` | 85% | Medium | Converts a wide character to a multibyte character using the specified locale. | MSVC6 CRT. Uses `CRT_mb_cur_max`. |

#### File I/O

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `CRT__unlock_file` | `0x1001bbb2` | 95% | High | Unlocks a file stream using its pointer to find the corresponding lock. | MSVC6 CRT |
| `CRT__unlock_fileno` | `0x1001bbe1` | 95% | High | Unlocks a file stream using its ID to find the corresponding lock. | MSVC6 CRT |
| `CRT_close` | `0x1001bc04` | 100% | High | A wrapper around `CRT_close_handle` that performs checks and sets `errno`. | MSVC6 CRT. Renamed from `close_file_handle`. |
| `CRT_close_handle` | `0x1001bc61` | 100% | High | The core function for closing a file handle. It calls the Windows `CloseHandle` API. | MSVC6 CRT. Renamed from `close_file_handle_2`. |
| `CRT_open` | `0x1002044c` | 90% | High | Opens or creates a file. It's a complex function that handles various flags and uses the Windows `CreateFileA` API. | MSVC6 CRT. Renamed from `file_management_16`. |
| `CRT_alloc_handle` | `0x10020142` | 90% | High | Allocates a new file handle from a global table. | MSVC6 CRT. Renamed from `file_management_9`. |
| `CRT_set_handle` | `0x10020265` | 95% | High | Associates a file handle with a file descriptor. | MSVC6 CRT. Renamed from `file_management_10`. |
| `CRT_free_handle` | `0x100202e1` | 95% | High | Disassociates a file handle from a file descriptor. | MSVC6 CRT. Renamed from `file_management_11`. |
| `CRT_get_handle` | `0x10020360` | 100% | High | Retrieves the file handle associated with a file descriptor. | MSVC6 CRT. Renamed from `file_management_12`. |
| `CRT_lock_handle` | `0x100203a2` | 100% | High | Locks a file handle using a critical section. | MSVC6 CRT. Renamed from `file_management_13`. |
| `CRT_unlock_handle` | `0x10020401` | 100% | High | Unlocks a file handle. | MSVC6 CRT. Renamed from `file_management_14`. |
| `CRT_is_char_device` | `0x10020423` | 100% | High | Checks if a file is a character device. | MSVC6 CRT. Renamed from `file_management_15`. |
| `CRT_flush_all` | `0x1001ad32` | 90% | High | Flushes the buffers of all open file streams. | MSVC6 CRT. Renamed from `file_management`. |
| `CRT_fclose` | `0x1001a18a` | 100% | High | A wrapper around `__fclose_lk` that handles stream locking. | MSVC6 CRT. Renamed from `fclose_wrapper`. |
| `CRT_flush` | `0x1001ac9f` | 95% | High | A wrapper around `CRT_flush_buffer` that also handles character devices. | MSVC6 CRT. Renamed from `file_flush`. |
| `CRT_flush_buffer` | `0x1001accd` | 90% | High | The core function for flushing a file's buffer. | MSVC6 CRT. Renamed from `file_flush_2`. |
| `CRT_init_stream` | `0x1001bd0f` | 90% | High | Initializes a file stream, including allocating a buffer for it. | MSVC6 CRT. Renamed from `file_io`. |
| `CRT_flush_and_reset_buffer` | `0x1001bd9c` | 90% | High | Flushes a file's buffer and resets its state if the file is in an error state. | MSVC6 CRT. Renamed from `file_io_2`. |
| `CRT_lseek` | `0x1001cbb5` | 100% | High | A wrapper around `CRT_lseek_nolock` that locks the file handle. | MSVC6 CRT. Renamed from `file_io_5`. |
| `CRT_lseek_nolock` | `0x1001cc1a` | 95% | High | The core function for seeking within a file. It uses the Windows `SetFilePointer` API. | MSVC6 CRT. Renamed from `file_io_6`. |
| `CRT_fgetc` | `0x1001ede5` | 90% | High | Reads a character from a file, handling buffering and error checking. | MSVC6 CRT. Renamed from `file_io_15`. |
| `CRT_read` | `0x1001eec1` | 100% | High | A wrapper around `CRT_read_nolock` that locks the file handle. | MSVC6 CRT. Renamed from `file_io_16`. |
| `CRT_read_nolock` | `0x1001ef26` | 85% | Medium | The core function for reading from a file. It uses the Windows `ReadFile` API and handles various edge cases. | MSVC6 CRT. Renamed from `file_io_17`. |
| `CRT_flush_file_buffers` | `0x1001f0ff` | 95% | High | Flushes the buffers of a file to disk using the Windows `FlushFileBuffers` API. | MSVC6 CRT. Renamed from `file_io_22`. |
| `CRT_alloc_buffer` | `0x1002071b` | 90% | High | Allocates a buffer for a file stream. | MSVC6 CRT. Renamed from `file_io_31`. |
| `CRT_chsize` | `0x10022190` | 85% | Medium | Extends a file to a specified size by writing zeros to the end of the file. | MSVC6 CRT. Renamed from `file_io_48`. |
| `CRT_fputc` | `0x1001add6` | 95% | High | Writes a character to a file, handling buffering. | MSVC6 CRT. Renamed from `file_putc`. |
| `CRT_fread` | `0x1001aa6a` | 100% | High | A wrapper around `CRT_fread_nolock` that locks the file stream. | MSVC6 CRT. Renamed from `file_read_3`. |
| `CRT_fread_nolock` | `0x1001aa99` | 85% | Medium | The core function for reading from a file. It handles buffering and calls `CRT_read` to perform the actual read operation. | MSVC6 CRT. Renamed from `file_read_4`. |
| `CRT_fseek` | `0x1001a49a` | 95% | High | A wrapper around `CRT_lseek` that handles buffering and error checking. | MSVC6 CRT. Renamed from `file_seek_2`. |
| `CRT_write` | `0x1001e8b4` | 100% | High | A wrapper around `CRT_write_nolock` that locks the file handle. | MSVC6 CRT. Renamed from `file_write_11`. |
| `CRT_write_nolock` | `0x1001e919` | 85% | Medium | The core function for writing to a file. It uses the Windows `WriteFile` API and handles various edge cases. | MSVC6 CRT. Renamed from `file_write_12`. |
| `CRT_fwrite` | `0x1001a960` | 85% | Medium | The core function for writing to a file. It handles buffering and calls `CRT_write` to perform the actual write operation. | MSVC6 CRT. Renamed from `file_write_2`. |

#### Environment

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `CRT_putenv` | `0x10023535` | 85% | Medium | Adds or modifies an environment variable. | MSVC6 CRT |
| `CRT__findenv` | `0x100236bc` | 90% | High | Finds an environment variable in the environment table. | MSVC6 CRT |
| `CRT__clone_environ` | `0x10023714` | 90% | High | Creates a copy of the environment table. | MSVC6 CRT |
| `CRT_getenv` | `0x10022340` | 95% | High | Gets an environment variable. | MSVC6 CRT |
| `CRT_GetEnvironmentStrings` | `0x1001fcc6` | 95% | High | Gets the environment strings from the OS, either in wide-character or multi-byte format. It then converts them to multi-byte if necessary and stores them in a buffer. | MSVC6 CRT |
| `CRT_reset_locale_info` | `0x10021f3d` | 95% | High | Resets the locale information of the C runtime. It clears a large block of memory and resets several global variables related to locale settings. | MSVC6 CRT |

#### Time

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `CRT_GetLocalTime` | `0x1001a567` | 95% | High | Gets the current local time and caches the result. This function also handles daylight saving time. | MSVC6 CRT |

#### Type Conversion

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `CRT_atof` | `0x1001f20b` | 80% | Medium | Converts a string to a floating-point number. | MSVC6 CRT |
| `CRT__atof_l` | `0x1002255e` | 75% | Medium | Converts a string to a floating-point number using the specified locale. | MSVC6 CRT |
| `CRT_atoi` | `0x10020fe1` | 100% | High | Converts a string to an integer. | MSVC6 CRT |
| `CRT_strtol` | `0x10020ff8` | 85% | Medium | Converts a string to a long integer. | MSVC6 CRT |
| `CRT__atoi_l` | `0x100222b5` | 90% | High | Converts a string to an integer using the specified locale. | MSVC6 CRT |
| `CRT__gcvt` | `0x1001f309` | 80% | Medium | Converts a floating-point number to a string. | MSVC6 CRT |
| `CRT_gcvt_s` | `0x1001f36a` | 80% | Medium | Converts a floating-point number to a string with scientific notation. | MSVC6 CRT |
| `CRT__fcvt` | `0x1001f42c` | 80% | Medium | Converts a floating-point number to a string. | MSVC6 CRT |
| `CRT_fcvt_s` | `0x1001f481` | 80% | Medium | Converts a floating-point number to a string with a specified number of digits after the decimal point. | MSVC6 CRT |
| `CRT__ecvt` | `0x1001f528` | 80% | Medium | Converts a floating-point number to a string. | MSVC6 CRT |

#### Process Control

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `CRT__errno` | `0x1001a7e5` | 100% | High | Returns a pointer to the thread-local `errno` value. | MSVC6 CRT |
| `CRT___doserrno` | `0x1001a7ee` | 100% | High | Returns a pointer to the thread-local `_doserrno` value. | MSVC6 CRT |
| `CRT_exit` | `0x1001fe40` | 100% | High | The standard C exit function. | MSVC6 CRT |
| `CRT__cexit` | `0x1001fe60` | 100% | High | Performs cleanup tasks and returns. | MSVC6 CRT |
| `CRT__exit` | `0x1001fdf0` | 100% | High | Terminates the calling process. | MSVC6 CRT |
| `CRT__initterm` | `0x1001fdd0` | 100% | High | Calls registered atexit handlers or global C++ destructors. | MSVC6 CRT |
| `CRT__lock` | `0x1001ffc0` | 100% | High | Acquires a lock to prevent race conditions during exit processing. | MSVC6 CRT |
| `CRT__unlock` | `0x1001ffd0` | 100% | High | Releases the lock acquired by lock_exit(). | MSVC6 CRT |
| `CRT_atexit` | `0x1001fe80` | 90% | High | This is a common exit function used by exit() and _cexit(). It handles calling atexit handlers and other cleanup tasks. | MSVC6 CRT |
| `CRT_Startup10` | `0x1001f192` | 100% | High | Performs C runtime startup initialization, likely related to memory management or bitwise operations. | MSVC6 CRT |

### zlib 1.1.3

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `zlib_adler32` | `0x10001000` | 100% | High | See zlib documentation. | Statically linked. From adler32.c, line 33. |
| `zlib_crc32` | `0x100011f0` | 100% | High | See zlib documentation. | Statically linked. From crc32.c, line 186. |
| `zlib_deflateInit2_` | `0x10001330` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 204. |
| `zlib_deflateReset` | `0x10001530` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 288. |
| `zlib_deflate` | `0x100015b0` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 388. |
| `zlib_deflateEnd` | `0x10001910` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 508. |
| `zlib_deflate_stored` | `0x10001a60` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 681. |
| `zlib_fill_window` | `0x10001bc0` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 868. |
| `zlib_read_buf` | `0x10001cf0` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 365. |
| `zlib_parseGzipHeader` | `0x100036d0` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 186. |
| `zlib_getByte` | `0x10003820` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 161. |
| `zlib_closeFile` | `0x100038a0` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 455. |
| `zlib_readFromStream` | `0x10003960` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 293. |
| `zlib_writeToStream` | `0x10003b90` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 365. |
| `zlib_getLong` | `0x10003c50` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 485. |
| `zlib_closeStream` | `0x10003ca0` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 455. |
| `zlib_putLong` | `0x10003cf0` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 474. |
| `zlib_inflateReset` | `0x10003d20` | 100% | High | See zlib documentation. | Statically linked. From inflate.c, line 65. |
| `zlib_inflateInit2_` | `0x10003da0` | 100% | High | See zlib documentation. | Statically linked. From inflate.c, line 88. |
| `zlib_inflate` | `0x10003e40` | 100% | High | See zlib documentation. | Statically linked. From inflate.c, line 153. |
| `zlib_inflateEnd` | `0x10004b40` | 100% | High | See zlib documentation. | Statically linked. From inflate.c, line 76. |
| `zlib_tr_init` | `0x10004b80` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 505. |
| `zlib_inflate_codes` | `0x10004bc0` | 100% | High | See zlib documentation. | Statically linked. From infcodes.c, line 101. |
| `zlib_inflate_trees_free` | `0x10005370` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 418. |
| `zlib_inflate_fast` | `0x10005390` | 100% | High | See zlib documentation. | Statically linked. From inffast.c, line 28. |
| `zlib_inflate_blocks_reset` | `0x10005720` | 100% | High | See zlib documentation. | Statically linked. From infblock.c, line 158. |
| `zlib_inflate_blocks_free` | `0x10005770` | 100% | High | See zlib documentation. | Statically linked. From infblock.c, line 426. |
| `zlib_inflate_blocks_new` | `0x100057c0` | 100% | High | See zlib documentation. | Statically linked. From infblock.c, line 178. |
| `zlib_inflate_blocks` | `0x100058d0` | 100% | High | See zlib documentation. | Statically linked. From infblock.c, line 201. |
| `zlib_inflate_trees_dynamic` | `0x10005d00` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 353. |
| `zlib_huft_build` | `0x10005db0` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 88. |
| `zlib_inflate_trees_bits` | `0x10006280` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 329. |
| `zlib_inflate_trees_fixed` | `0x10006410` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 438. |
| `zlib_inflate_flush` | `0x10006440` | 100% | High | See zlib documentation. | Statically linked. From infutil.c, line 25. |
| `zlib_ct_init` | `0x10006ec0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 505. |
| `zlib_tr_tally` | `0x10006f40` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 813. |
| `zlib_tr_flush_block` | `0x10006fb0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 861. |
| `zlib_ct_tally` | `0x10007050` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 813. |
| `zlib_bi_flush` | `0x100072b0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 1014. |
| `zlib_build_tree` | `0x100074a0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 678. |
| `zlib_pqdownheap` | `0x100076e0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 573. |
| `zlib_gen_codes` | `0x100077c0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 644. |
| `zlib_gen_bitlen` | `0x100079f0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 598. |
| `zlib_build_static_trees` | `0x10007a70` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 505. |
| `zlib_scan_tree` | `0x10007ae0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 724. |
| `zlib_send_tree` | `0x10007bd0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 765. |
| `zlib_send_codes` | `0x10007e40` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 914. |
| `zlib_send_all_trees` | `0x100083c0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 833. |
| `zlib_build_bl_tree` | `0x10008800` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 801. |
| `zlib_bi_reverse` | `0x10008880` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 997. |
| `zlib_bi_windup` | `0x100088a0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 1029. |
| `zlib_bi_align` | `0x10008930` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 850. |
| `zlib_tr_stored_block` | `0x100089b0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 943. |
| `zlib_write_to_buffer` | `0x10001860` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 62. |
| `zlib_flush_buffer` | `0x10001890` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 75. |
| `zlib_reset_data` | `0x100019c0` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 299. |
| `zlib_zcalloc` | `0x100092e0` | 100% | High | See zlib documentation. | Statically linked. From zutil.c, line 264. |
