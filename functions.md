# Functions

## Exports

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `Init` | `0x10009320` | 100% | High | Server entry point. Creates the main game loop thread. | Exported function. |
| `Exit` | `0x10009350` | 100% | High | Server exit point. Terminates the game loop thread. | Exported function. |

## Server Core (`srv_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `srv_GameLoop` | `0x100093a0` | 70% | Medium | Main server loop. Manages clients, game state, and network traffic. | Core of the server logic. Needs further analysis of sub-functions. |
| `srv_InitServer` | `0x10009d30` | 90% | High | Initializes server components like error handling, memory, and game data. | Called once at the start of the game loop. |
| `srv_InitSockets` | `0x10009e60` | 95% | High | Initializes the main server socket for network communication. | Uses Winsock API. |
| `srv_AcceptClient` | `0x1000a080` | 85% | High | Accepts new client connections and assigns them to a slot. | Handles the initial client handshake. |
| `srv_ProcessClientCommands` | `0x1000a570` | 80% | Medium | Processes incoming commands from clients. | Dispatches commands based on their type. |
| `srv_RecvFromClient` | `0x1000a340` | 90% | High | Receives data from a client connection. | Handles timeouts and Winsock errors. |
| `srv_DispatchGameCommand` | `0x1000aac0` | 80% | Medium | Dispatches game commands to their appropriate handlers. | Uses a jump table to call command handlers. |
| `srv_HandlePlayerCommand` | `0x10010390` | 80% | Medium | Command handler for player-related commands. | Dispatches to sub-handlers based on a command ID. |
| `srv_LoadGameState` | `0x10014260` | 70% | Medium | Receives and loads the game state from a file. | Reads player, building, dynasty, alchemist, and town data. |
| `send_broadcast_message` | `0x10001130` | 90% | High | Sends a UDP broadcast message. | Likely used for server discovery. |

## Command Handlers (`cm_`, `cm_Ex`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `cm_ExAllocGebaeude` | `0x1000d350` | 85% | High | Command handler for allocating a new building. | Calls `gm_AllocBuilding` to perform the allocation. |
| `cm_ExAllocSpieler` | `0x1000d460` | 85% | High | Command handler for allocating a new player. | Calls `gm_AllocPlayer` to perform the allocation. |
| `cm_ExMoveObject` | `0x1000d8a0` | 85% | High | Command handler for moving an object. | Calls `gm_RemoveObjectNoKill` and `gm_AddObject`. |
| `cm_ExSellObject` | `0x1000d7f0` | 85% | High | Command handler for selling an object. | Calls `gm_RemoveObject` and `gm_AddObject`. |
| `cm_ExProdObjekt` | `0x1000e140` | 80% | Medium | Command handler for producing an object. | Handles the crafting and production system. |
| `cm_KillPlayer` | `0x1000f030` | 85% | High | Command handler for killing a player. | Calls `gm_KillSpieler` to perform the action. |
| `cm_EmployWorker` | `0x1000f730` | 80% | Medium | Command handler for employing a worker. | Handles the creation of new workers. |
| `cm_CreateBuilding` | `0x1000fb30` | 85% | High | Command handler for creating a building. | Calls `gm_AllocBuilding` to perform the action. |
| `cm_SetPlayerMoney` | `0x1000ffc0` | 90% | High | Sets a player's money. | Updates the player's money value. |
| `cm_SetPlayerTitle` | `0x10010010` | 90% | High | Sets a player's title. | Updates the player's title and Amt information. |
| `cm_SetPlayerSkill` | `0x100100a0` | 90% | High | Sets a player's skill. | Updates the player's skill value. |
| `cm_StartCutscene` | `0x1000ff60` | 85% | High | Command handler for starting a cutscene. | Calls `cm_IsCutsceneReady` and sets player flags. |
| `cm_ZombieCommand` | `0x10010260` | 95% | High | Command handler for zombie-related commands. | Dispatches to sub-handlers based on a command ID. |
| `cm_AllocGraveyardWorker` | `0x10010310` | 90% | High | Command handler for allocating a graveyard worker. | Calls `handleAllocGraveyardWorker2`. |
| `cm_GetPlayerAmtId` | `0x10010350` | 90% | High | Command handler for getting a player's "Amt" ID. | Calls `handleGetPlayerAmtId`. |
| `cm_ExGetBuildingDataSize` | `0x100104a0` | 90% | High | Command handler for getting the size of a building's data. | Returns the size of a building's data structure. |
| `cm_ExValidateBuildingData` | `0x10010530` | 90% | High | Command handler for validating a building's data. | Validates specific fields within a building's data structure. |
| `cm_ExGetBuildingDataPtr` | `0x100105b0` | 90% | High | Command handler for getting a pointer to a building's data. | Returns a pointer to the requested data. |
| `cm_ExIterateBuildingData` | `0x10010710` | 85% | High | Command handler for iterating over a building's data. | Iterates through building data and calls a callback. |
| `cm_ExAllocGraveyard` | `0x10010850` | 80% | Medium | Command handler for allocating a graveyard. | Allocates and initializes a graveyard building. |
| `cm_ExAllocGraveyardField` | `0x100109d0` | 80% | Medium | Command handler for allocating a graveyard field. | Allocates and initializes a graveyard field within a building. |
| `cm_ExChangePlayerIdentity` | `0x1000d6e0` | 90% | High | Command handler for changing a player's identity. | Calls `gm_ChangePlayerIdentity` to perform the change. |
| `cm_ExFree` | `0x1000d730` | 85% | High | Command handler for freeing a player or building. | Calls `gm_KillSpieler` or `gm_FreeBuilding`. |
| `cm_ExSellObjekt` | `0x1000d930` | 75% | Medium | Command handler for selling an object with extended functionality. | Complex logic for handling various sale scenarios. |
| `cm_ExClearLagerslot` | `0x1000e690` | 85% | High | Command handler for clearing a storage slot. | Calls `handleRemoveObjectFromList`. |
| `cm_ExChangeDesire` | `0x1000e9c0` | 85% | High | Command handler for changing a player's desire. | Updates and clamps desire values. |
| `cm_ExchangeBits` | `0x1000eaa0` | 90% | High | Command handler for exchanging bits between players. | Updates player data based on size and offset. |
| `cm_ExchangeFloat` | `0x1000eb70` | 90% | High | Command handler for exchanging a float value between players. | Updates player data at a given offset. |
| `cm_AllocCharacter` | `0x1000f980` | 85% | High | Command handler for allocating a new character. | Calls `gm_AllocPlayer` to create a new character. |
| `cm_CanBuyItem` | `0x1000d060` | 85% | High | Checks if an item can be purchased. | Handles special item types and prevents duplicate purchases. |
| `cm_ValidateLobbyAction` | `0x1000d110` | 80% | Medium | Validates lobby actions like joining and leaving. | Uses a 4-byte identifier to determine the action. Return logic is inverted. |
| `cm_IsCutsceneReady` | `0x1000d260` | 85% | High | Checks if a cutscene is ready to be played. | Iterates through players and checks their status. |
| `cm_Stub` | `0x1000d330` | 100% | High | Stub function that does nothing. | Placeholder for an unimplemented command. |
| `cm_NotYetImplemented` | `0x1000d340` | 100% | High | Stub function that does nothing. | Placeholder for an unimplemented command. |
| `cm_ExAllocObject` | `0x1000e750` | 85% | High | Command handler for allocating a new object. | Calls `gm_AllocObject` to perform the allocation. |
| `cm_ExSetAttribute` | `0x1000e8d0` | 85% | High | Command handler for setting an attribute on a game object. | Can be used to modify a wide range of game data. |
| `cm_AdjustRelationship` | `0x1000ec00` | 70% | Medium | Adjusts the relationship between two players. | Complex logic with different calculations based on adjustment type. |

## Game Mechanics (`gm_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `gm_AllocBuilding` | `0x100174d0` | 80% | Medium | Allocates and initializes a new building. | Manages the building data pool. |
| `gm_GetFreeBuildingSlot` | `0x10017210` | 95% | High | Retrieves a free building slot from the building data pool. | Simple linear search. |
| `gm_AllocRoom` | `0x10017c40` | 80% | Medium | Allocates and initializes a new room within a building. | Creates associated objects. |
| `gm_AllocObject` | `0x10016760` | 80% | Medium | Allocates and initializes a new game object. | Core function for creating game entities. |
| `gm_AllocPlayer` | `0x10018850` | 75% | Medium | Allocates and initializes a new player. | Manages the player data pool and initializes player attributes. |
| `gm_RemoveObjectNoKill` | `0x10016ea0` | 90% | High | Removes an object from a list without deallocating it. | Used for moving objects between containers. |
| `gm_AddObject` | `0x10016cd0` | 90% | High | Adds an object to a list, or updates its count if it already exists. | Used for moving objects between containers. |
| `gm_RemoveObject` | `0x10016de0` | 90% | High | Removes an object from a list. | Used for selling objects. |
| `gm_GetBuildingItemCount` | `0x10019cd0` | 95% | High | Retrieves the item count of a building. | Has special handling for certain item types. |
| `gm_IsBuildingInventoryFull` | `0x10019d30` | 85% | High | Checks if a building's inventory is full. | Prevents players from exceeding storage capacity. |
| `gm_KillSpieler` | `0x10017fb0` | 80% | Medium | Kills a player and performs cleanup. | Removes the player from the game world. |

## Load/Save (`ls_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `ls_ID2Ptr` | `0x10014070` | 60% | Low | Converts IDs to pointers after loading data. | Resolves references between game objects. |

## Lobby (`lobby_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `lobby_get_player_list` | `0x100145e0` | 90% | High | Retrieves the list of players in the lobby. | Sends the list of player IDs to the requesting client. |
| `lobby_set_player_ready_status` | `0x100146c0` | 90% | High | Sets the ready status of a player in the lobby. | Broadcasts the new status to all clients in the lobby. |
| `lobby_join_game` | `0x100147b0` | 85% | High | Allows a player to join the game from the lobby. | Assigns the player to a slot and broadcasts the updated player list. |
| `lobby_update_player_status` | `0x10014a50` | 90% | High | Updates the status of a player in the lobby. | Broadcasts the new status to all clients in the lobby. |

## Simulation (`sim_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `sim_UpdateCitizenAge` | `0x100155c0` | 90% | High | Updates a citizen's age. | Adds days, months, and years to a citizen's age. |
| `sim_SetCitizenData` | `0x10015690` | 95% | High | Sets a citizen's data. | Sets the gender, age, and birth year of a citizen. |

## Memory Management (`m_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `m_alloc` | `0x10006580` | 70% | Medium | Custom memory allocation function. | Tracks memory usage with tags and statistics. |
| `m_free` | `0x10006820` | 85% | High | Custom memory deallocation function. | Checks for double-free and memory underflow errors. |
| `m_alloc_init` | `0x100068e0` | 90% | High | Initializes the custom memory allocator. | Allocates the tracking table and initializes statistics. |
| `m_alloc_dump` | `0x10006990` | 80% | Medium | Dumps memory allocation statistics to the log. | Can be filtered by tag for targeted debugging. |
| `m_alloc_cleanup` | `0x10006c00` | 90% | High | Cleans up the custom memory allocator. | Frees all tracked memory and reports leaks. |
| `m_pool_alloc` | `0x10006d20` | 80% | Medium | Allocates memory from a memory pool. | Efficiently allocates fixed-size objects. |
| `m_pool_free` | `0x10006e30` | 85% | High | Frees a block of memory from a memory pool. | Includes checks for invalid free attempts. |

## File System (`file_`, `vfs_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `file_close` | `0x10008a50` | 90% | High | Closes a file and frees its associated memory. | Also calls `file_close_and_free` if a certain flag is set. |
| `file_read` | `0x10008a90` | 75% | Medium | Reads data from a file, handling both compressed and uncompressed data. | Manages buffers, CRC32 checks, and zlib inflation. |
| `file_close_and_free` | `0x10008c80` | 90% | High | Closes a file and frees its associated memory, including the zlib inflate stream. | Used for compressed files. |
| `file_read_data` | `0x10008d10` | 70% | Medium | High-level function for reading data from files. | Handles different file types and compression, and performs cleanup. |
| `vfs_read` | `0x10008e40` | 70% | Medium | Reads data from a virtual file system (VFS) entry. | Handles different file types and compression. |
| `vfs_open` | `0x10009020` | 75% | Medium | Opens a virtual file system (VFS) entry for reading or writing. | Supports compressed and uncompressed data. |

## Office/Rank (`amt_`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `is_amt_valid` | `0x1000d020` | 95% | High | Checks if an 'Amt' (office/rank) is valid. | Wrapper for `validate_amt`. |
| `validate_amt` | `0x1000b1c0` | 70% | Medium | Validates an 'Amt' (office/rank) entry. | Complex logic involving multiple global data structures. |
| `is_amt_action_valid` | `0x1000d040` | 95% | High | Checks if an 'Amt' (office/rank) action is valid. | Wrapper for `handleValidateAmtAction`. |
| `handleValidateAmtAction` | `0x1000b440` | 70% | Medium | Validates an 'Amt' (office/rank) action. | Complex logic involving multiple global data structures. |

## Handlers (`handle`)

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `handle_invalid_command` | `0x1000d2e0` | 95% | High | Handles invalid or unknown commands. | Logs an error message. |
| `handleGetPlayerById` | `0x100184a0` | 95% | High | Retrieves a player's data by their ID. | Simple linear search. |
| `handleGetPlayerClass` | `0x10018200` | 95% | High | Retrieves the class of a player based on their type. | Uses a switch statement to map player type to class. |
| `handleGetRandomPlayerAttribute` | `0x10018450` | 95% | High | Generates a random player attribute based on a base value. | Used for character creation. |
| `handleCreateCitizen2` | `0x10015500` | 85% | High | Creates a new citizen with specified properties. | Used by `cm_EmployWorker` to create new workers. |

## Internal/System

| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `enqueue_client_command` | `0x1000a8f0` | 90% | High | Queues a command to be sent to a client. | Manages the outgoing command buffer. |
| `client_queue_append_command` | `0x1000a9a0` | 90% | High | Queues a command to be sent to a client. | This function adds a command to a client's outgoing queue, but it does not send it. It is the responsibility of the caller to eventually send the command. |
| `dequeue_command` | `0x1000aa50` | 90% | High | Dequeues a command from a client's incoming queue. | Manages the incoming command buffer. |
| `logEvent` | `0x10002640` | 90% | High | Logs a message to a file, debug output, and/or console. | Game-specific utility function. |
| `unhandledExceptionHandler` | `0x10002770` | 75% | Medium | Unhandled exception filter that generates a crash dump. | Critical for server stability and debugging. |
| `writeArchiveFile` | `0x10002fc0` | 70% | Medium | Writes data to an archive file, likely for crash dumps. | Part of the error handling and debugging system. |
| `getDataBlock` | `0x10003140` | 85% | High | Retrieves a data block from a data structure. | Used by the crash dump generation system. |
| `checkMemoryProtection` | `0x10003170` | 85% | High | Checks the memory protection of a given address. | Used by the crash dump generation system. |
| `analyzeBytePattern` | `0x10003260` | 80% | Medium | Analyzes a byte pattern to identify function prologues. | Used by the crash dump generation system to improve stack traces. |
| `errorHandlerInit` | `0x10003320` | 90% | High | Initializes the error handling for the application. | Sets up the unhandled exception filter and logging. |
| `errorHandlerCleanup` | `0x100034c0` | 90% | High | Cleans up the error handling system. | Logs a final message and frees the console if allocated. |
| `fatalError` | `0x10003520` | 90% | High | Handles fatal errors. | Logs the error, displays a message box, and can terminate the program. |
| `showMessage` | `0x100035c0` | 95% | High | Displays a message to the user. | Can log to a file or display a message box. |
| `logMessage` | `0x10003640` | 95% | High | Logs a message with file and line number information. | Valuable for debugging. |
| `DllMain_Internal` | `0x10009310` | 100% | High | Internal DllMain function. | Stub function that returns 1. |
