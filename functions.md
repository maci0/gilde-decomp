# Functions

## Exports

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `Init` | `0x10009320` | 100% | High | Server entry point. Creates the main game loop thread. | Exported function. |
| `Exit` | `0x10009350` | 100% | High | Server exit point. Terminates the game loop thread. | Exported function. |

## Server Core (`srv_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `srv_GameLoop` | `0x100093a0` | 90% | High | The main server loop. After calling `srv_InitServer`, it enters a `while` loop controlled by `g_bShutdownFlag`. In each iteration, it calls `srv_AcceptClient`, `srv_ProcessClientCommands`, and `srv_LoadGameState`. It yields execution with `Sleep(1)`. | Core of the server logic. Handles the entire game lifecycle from initialization to shutdown. |
| `srv_InitServer` | `0x10009d30` | 100% | High | Initializes the server's core components. It sets the thread priority, initializes the custom memory allocator (`m_alloc_init`), loads game data (`amt_fio_LoadAemter`), and initializes network sockets (`srv_InitSockets`). | This is a critical function called once at the beginning of the `srv_GameLoop`. It orchestrates the entire server setup. |
| `srv_InitSockets` | `0x10009e60` | 100% | High | Initializes the server's network sockets using Winsock. It follows the standard sequence: `WSAStartup`, `socket`, `setsockopt` (SO_REUSEADDR, SO_RCVBUF, SO_SNDBUF), `bind`, and `listen`. | A core networking function that prepares the server to accept client connections. |
| `srv_AcceptClient` | `0x1000a080` | 90% | High | Accepts new client connections non-blockingly using `select`. If a connection is pending, it calls `accept` and assigns the new client to a free slot. | Handles the initial client handshake efficiently without blocking the main loop. |
| `srv_ProcessClientCommands` | `0x1000a570` | 85% | High | Processes incoming commands from all connected clients. It iterates through the client list, calls `srv_RecvFromClient` to read data, and then dispatches the received commands using `srv_DispatchGameCommand`. | Manages the flow of all incoming client data. |
| `srv_RecvFromClient` | `0x1000a340` | 95% | High | Receives data from a client connection using a non-blocking `select`. It reads the command header to determine the message size and then reads the full message. | Handles timeouts and Winsock errors gracefully. Appears to handle message framing. |
| `srv_DispatchGameCommand` | `0x1000aac0` | 90% | High | Dispatches game commands to their appropriate handlers using a large jump table (switch statement). It reads a command ID from the client's stream and calls the corresponding `cm_*` function. | The central command router for the server. |
| `srv_HandlePlayerCommand` | `0x10010390` | 85% | Medium | A secondary command dispatcher specifically for player-related commands. It takes a subcommand ID and calls the appropriate handler. | Focuses on player-specific actions. |
| `srv_LoadGameState` | `0x10014260` | 70% | Medium | Receives and loads the complete game state from a client (likely the host). It reads a large, complex data structure containing all game objects and then calls `ls_ID2Ptr` to resolve pointers. | A critical, complex function for game state synchronization. |
| `send_broadcast_message` | `0x10001130` | 95% | High | Sends a UDP broadcast message to `255.255.255.255` for server discovery on the local network. It creates a UDP socket and sets the `SO_BROADCAST` option. | Standard implementation for LAN server discovery. |

## Command Handlers (`cm_`, `cm_Ex`)

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
| `cm_SetPlayerMoney` | `0x1000ffc0` | 100% | High | Sets a player's money. It directly updates the player's money value in the player data structure. | A simple and direct data modification. |
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

## Game Mechanics (`gm_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
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

## Load/Save (`ls_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `ls_ID2Ptr` | `0x10014070` | 65% | Medium | Converts object IDs to direct memory pointers after loading the game state. This is a critical step for resolving references between all game objects. | A complex function that is not yet fully understood. |

## Lobby (`lobby_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `lobby_get_player_list` | `0x100145e0` | 95% | High | Retrieves the list of players in the lobby and sends it to the requesting client. | Renamed variables for clarity. |
| `lobby_set_player_ready_status` | `0x100146c0` | 95% | High | Sets the ready status of a player in the lobby and broadcasts the new status to all clients. | Renamed variables for clarity. |
| `lobby_join_game` | `0x100147b0` | 90% | High | Allows a player to join the game from the lobby. It assigns the player to a slot and broadcasts the updated player list. | Renamed variables for clarity. |
| `lobby_update_player_status` | `0x10014a50` | 95% | High | Updates the status of a player in the lobby and broadcasts the new status to all clients. | Renamed variables for clarity. |

## Simulation (`sim_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `sim_UpdateCitizenAge` | `0x100155c0` | 95% | High | Updates a citizen's age. It adds days, months, and years to a citizen's age. | Renamed variables for clarity. |
| `sim_SetCitizenData` | `0x10015690` | 100% | High | Sets a citizen's data. It sets the gender, age, and birth year of a citizen. | A simple and direct data modification. |

## Memory Management (`m_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `m_alloc` | `0x10006580` | 75% | Medium | Custom memory allocation function. It tracks memory usage with tags and statistics, and it includes checks for common memory errors. | Renamed variables for clarity. |
| `m_free` | `0x10006820` | 90% | High | Custom memory deallocation function. It includes checks for double-free and memory underflow errors. | Renamed variables for clarity. |
| `m_alloc_init` | `0x100068e0` | 95% | High | Initializes the custom memory allocator. It allocates the tracking table and initializes statistics. | Renamed variables for clarity. |
| `m_alloc_dump` | `0x10006990` | 85% | Medium | Dumps memory allocation statistics to the log. It can be filtered by tag for targeted debugging. | A useful debugging tool. |
| `m_alloc_cleanup` | `0x10006c00` | 95% | High | Cleans up the custom memory allocator. It frees all tracked memory and reports leaks. | Renamed variables for clarity. |
| `m_pool_alloc` | `0x10006d20` | 85% | Medium | Allocates memory from a memory pool. This is an efficient way to allocate fixed-size objects. | Renamed variables for clarity. |
| `m_pool_free` | `0x10006e30` | 90% | High | Frees a block of memory from a memory pool. It includes checks for invalid free attempts. | Renamed variables for clarity. |

## File System (`file_`, `vfs_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `file_close` | `0x10008a50` | 95% | High | Closes a file and frees its associated memory. It also calls `file_close_and_free` if a certain flag is set. | Renamed variables for clarity. |
| `file_read` | `0x10008a90` | 80% | Medium | Reads data from a file, handling both compressed and uncompressed data. It manages buffers, CRC32 checks, and zlib inflation. | A complex function that is central to file I/O. |
| `file_close_and_free` | `0x10008c80` | 95% | High | Closes a file and frees its associated memory, including the zlib inflate stream. This is used for compressed files. | Renamed variables for clarity. |
| `file_read_data` | `0x10008d10` | 75% | Medium | High-level function for reading data from files. It handles different file types and compression, and it performs cleanup. | Renamed variables for clarity. |
| `vfs_read` | `0x10008e40` | 75% | Medium | Reads data from a virtual file system (VFS) entry. It handles different file types and compression. | Renamed variables for clarity. |
| `vfs_open` | `0x10009020` | 80% | Medium | Opens a virtual file system (VFS) entry for reading or writing. It supports compressed and uncompressed data. | The entry point for all VFS operations. |

## Office/Rank (`amt_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `is_amt_valid` | `0x1000d020` | 100% | High | Checks if an 'Amt' (office/rank) is valid. It's a simple wrapper for `validate_amt`. | Renamed variables for clarity. |
| `validate_amt` | `0x1000b1c0` | 75% | Medium | Validates an 'Amt' (office/rank) entry. It contains complex logic involving multiple global data structures. | Requires further analysis to fully understand the validation logic. |
| `is_amt_action_valid` | `0x1000d040` | 100% | High | Checks if an 'Amt' (office/rank) action is valid. It's a simple wrapper for `handleValidateAmtAction`. | Renamed variables for clarity. |
| `handleValidateAmtAction` | `0x1000b440` | 75% | Medium | Validates an 'Amt' (office/rank) action. It contains complex logic involving multiple global data structures. | Requires further analysis to fully understand the validation logic. |

## Handlers (`handle`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `handle_invalid_command` | `0x1000d2e0` | 100% | High | Handles invalid or unknown commands by logging an error message. | A simple error handling function. |
| `handleGetPlayerById` | `0x100184a0` | 100% | High | Retrieves a player's data by their ID using a simple linear search. | Renamed variables for clarity. |
| `handleGetPlayerClass` | `0x10018200` | 100% | High | Retrieves the class of a player based on their type. It uses a switch statement to map the player type to a class. | Renamed variables for clarity. |
| `handleGetRandomPlayerAttribute` | `0x10018450` | 100% | High | Generates a random player attribute based on a base value. This is used for character creation. | Renamed variables for clarity. |
| `handleCreateCitizen2` | `0x10015500` | 90% | High | Creates a new citizen with specified properties. It is used by `cm_EmployWorker` to create new workers. | Renamed variables for clarity. |

## Internal/System

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `enqueue_client_command` | `0x1000a8f0` | 95% | High | Queues a command to be sent to a client. It manages the outgoing command buffer. | Renamed variables for clarity. |
| `client_queue_append_command` | `0x1000a9a0` | 95% | High | Queues a command to be sent to a client. This function adds a command to a client's outgoing queue, but it does not send it. | Renamed variables for clarity. |
| `dequeue_command` | `0x1000aa50` | 95% | High | Dequeues a command from a client's incoming queue. It manages the incoming command buffer. | Renamed variables for clarity. |
| `logEvent` | `0x10002640` | 95% | High | Logs a message to a file, debug output, and/or console. This is a game-specific utility function. | Renamed variables for clarity. |
| `unhandledExceptionHandler` | `0x10002770` | 80% | Medium | Unhandled exception filter that generates a crash dump. This is critical for server stability and debugging. | A complex but important function. |
| `writeArchiveFile` | `0x10002fc0` | 75% | Medium | Writes data to an archive file, likely for crash dumps. This is part of the error handling and debugging system. | Renamed variables for clarity. |
| `getDataBlock` | `0x10003140` | 90% | High | Retrieves a data block from a data structure. This is used by the crash dump generation system. | Renamed variables for clarity. |
| `checkMemoryProtection` | `0x10003170` | 90% | High | Checks the memory protection of a given address. This is used by the crash dump generation system. | Renamed variables for clarity. |
| `analyzeBytePattern` | `0x10003260` | 85% | Medium | Analyzes a byte pattern to identify function prologues. This is used by the crash dump generation system to improve stack traces. | A clever technique for improving crash reports. |
| `errorHandlerInit` | `0x10003320` | 95% | High | Initializes the error handling for the application. It sets up the unhandled exception filter and logging. | Renamed variables for clarity. |
| `errorHandlerCleanup` | `0x100034c0` | 95% | High | Cleans up the error handling system. It logs a final message and frees the console if allocated. | Renamed variables for clarity. |
| `fatalError` | `0x10003520` | 95% | High | Handles fatal errors. It logs the error, displays a message box, and can terminate the program. | Renamed variables for clarity. |
| `showMessage` | `0x100035c0` | 100% | High | Displays a message to the user. It can log to a file or display a message box. | A simple and direct utility function. |
| `logMessage` | `0x10003640` | 100% | High | Logs a message with file and line number information. This is valuable for debugging. | A simple and direct utility function. |
| `DllMain_Internal` | `0x10009310` | 100% | High | Internal DllMain function. It's a stub function that returns 1. | No analysis needed. |
