| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `Init` | `0x10009320` | 100% | High | Server entry point. Creates the main game loop thread. | Exported function. |
| `Exit` | `0x10009350` | 100% | High | Server exit point. Terminates the game loop thread. | Exported function. |
| `srv_GameLoop` | `0x100093a0` | 70% | Medium | Main server loop. Manages clients, game state, and network traffic. | Core of the server logic. Needs further analysis of sub-functions. |
| `srv_InitServer` | `0x10009d30` | 90% | High | Initializes server components like error handling, memory, and game data. | Called once at the start of the game loop. |
| `srv_InitSockets` | `0x10009e60` | 95% | High | Initializes the main server socket for network communication. | Uses Winsock API. |
| `srv_AcceptClient` | `0x1000a080` | 85% | High | Accepts new client connections and assigns them to a slot. | Handles the initial client handshake. |
| `srv_ProcessClientCommands` | `0x1000a570` | 80% | Medium | Processes incoming commands from clients. | Dispatches commands based on their type. |
| `srv_RecvFromClient` | `0x1000a340` | 90% | High | Receives data from a client connection. | Handles timeouts and Winsock errors. |
| `enqueue_client_command` | `0x1000a8f0` | 90% | High | Queues a command to be sent to a client. | Manages the outgoing command buffer. |
| `client_queue_append_command` | `0x1000a9a0` | 90% | High | Queues a command to be sent to a client. | This function adds a command to a client's outgoing queue, but it does not send it. It is the responsibility of the caller to eventually send the command. |
| `dequeue_command` | `0x1000aa50` | 90% | High | Dequeues a command from a client's incoming queue. | Manages the incoming command buffer. |
| `srv_DispatchGameCommand` | `0x1000aac0` | 80% | Medium | Dispatches game commands to their appropriate handlers. | Uses a jump table to call command handlers. |
| `handle_invalid_command` | `0x1000d2e0` | 95% | High | Handles invalid or unknown commands. | Logs an error message. |
| `cmdt_AllocBuilding` | `0x1000d350` | 85% | High | Command handler for allocating a new building. | Calls `gm_AllocBuilding` to perform the allocation. |
| `gm_AllocBuilding` | `0x100174d0` | 80% | Medium | Allocates and initializes a new building. | Manages the building data pool. |
| `gm_GetFreeBuildingSlot` | `0x10017210` | 95% | High | Retrieves a free building slot from the building data pool. | Simple linear search. |
| `gm_AllocRoom` | `0x10017c40` | 80% | Medium | Allocates and initializes a new room within a building. | Creates associated objects. |
| `gm_AllocObject` | `0x10016760` | 80% | Medium | Allocates and initializes a new game object. | Core function for creating game entities. |
| `cmdt_AllocPlayer` | `0x1000d460` | 85% | High | Command handler for allocating a new player. | Calls `gm_AllocPlayer` to perform the allocation. |
| `gm_AllocPlayer` | `0x10018850` | 75% | Medium | Allocates and initializes a new player. | Manages the player data pool and initializes player attributes. |
| `handleGetPlayerById` | `0x100184a0` | 95% | High | Retrieves a player's data by their ID. | Simple linear search. |
| `handleGetPlayerClass` | `0x10018200` | 95% | High | Retrieves the class of a player based on their type. | Uses a switch statement to map player type to class. |
| `handleGetRandomPlayerAttribute` | `0x10018450` | 95% | High | Generates a random player attribute based on a base value. | Used for character creation. |
| `cmdt_MoveObject` | `0x1000d8a0` | 85% | High | Command handler for moving an object. | Calls `gm_RemoveObjectNoKill` and `gm_AddObject`. |
| `gm_RemoveObjectNoKill` | `0x10016ea0` | 90% | High | Removes an object from a list without deallocating it. | Used for moving objects between containers. |
| `gm_AddObject` | `0x10016cd0` | 90% | High | Adds an object to a list, or updates its count if it already exists. | Used for moving objects between containers. |
| `cmdt_SellObject` | `0x1000d7f0` | 85% | High | Command handler for selling an object. | Calls `gm_RemoveObject` and `gm_AddObject`. |
| `gm_RemoveObject` | `0x10016de0` | 90% | High | Removes an object from a list. | Used for selling objects. |
| `cmdt_ProduceObject` | `0x1000e140` | 80% | Medium | Command handler for producing an object. | Handles the crafting and production system. |
| `gm_GetBuildingItemCount` | `0x10019cd0` | 95% | High | Retrieves the item count of a building. | Has special handling for certain item types. |
| `gm_IsBuildingInventoryFull` | `0x10019d30` | 85% | High | Checks if a building's inventory is full. | Prevents players from exceeding storage capacity. |
| `cm_KillPlayer` | `0x1000f030` | 85% | High | Command handler for killing a player. | Calls `gm_KillSpieler` to perform the action. |
| `gm_KillSpieler` | `0x10017fb0` | 80% | Medium | Kills a player and performs cleanup. | Removes the player from the game world. |
| `cm_EmployWorker` | `0x1000f730` | 80% | Medium | Command handler for employing a worker. | Handles the creation of new workers. |
| `handleCreateCitizen2` | `0x10015500` | 85% | High | Creates a new citizen with specified properties. | Used by `cm_EmployWorker` to create new workers. |
| `cm_CreateBuilding` | `0x1000fb30` | 85% | High | Command handler for creating a building. | Calls `gm_AllocBuilding` to perform the action. |
| `cm_SetPlayerMoney` | `0x1000ffc0` | 90% | High | Sets a player's money. | Updates the player's money value. |
| `cm_SetPlayerTitle` | `0x10010010` | 90% | High | Sets a player's title. | Updates the player's title and Amt information. |
| `cm_SetPlayerSkill` | `0x100100a0` | 90% | High | Sets a player's skill. | Updates the player's skill value. |
| `sim_UpdateCitizenAge` | `0x100155c0` | 90% | High | Updates a citizen's age. | Adds days, months, and years to a citizen's age. |
| `sim_SetCitizenData` | `0x10015690` | 95% | High | Sets a citizen's data. | Sets the gender, age, and birth year of a citizen. |
| `lobby_get_player_list` | `0x100145e0` | 90% | High | Retrieves the list of players in the lobby. | Sends the list of player IDs to the requesting client. |
| `lobby_set_player_ready_status` | `0x100146c0` | 90% | High | Sets the ready status of a player in the lobby. | Broadcasts the new status to all clients in the lobby. |
| `lobby_join_game` | `0x100147b0` | 85% | High | Allows a player to join the game from the lobby. | Assigns the player to a slot and broadcasts the updated player list. |
| `lobby_update_player_status` | `0x10014a50` | 90% | High | Updates the status of a player in the lobby. | Broadcasts the new status to all clients in the lobby. |
| `is_amt_valid` | `0x1000d020` | 95% | High | Checks if an 'Amt' (office/rank) is valid. | Wrapper for `validate_amt`. |
| `validate_amt` | `0x1000b1c0` | 70% | Medium | Validates an 'Amt' (office/rank) entry. | Complex logic involving multiple global data structures. |
| `is_amt_action_valid` | `0x1000d040` | 95% | High | Checks if an 'Amt' (office/rank) action is valid. | Wrapper for `handleValidateAmtAction`. |
| `handleValidateAmtAction` | `0x1000b440` | 70% | Medium | Validates an 'Amt' (office/rank) action. | Complex logic involving multiple global data structures. |
| `cm_CanBuyItem` | `0x1000d060` | 85% | High | Checks if an item can be purchased. | Handles special item types and prevents duplicate purchases. |
| `cm_ValidateLobbyAction` | `0x1000d110` | 80% | Medium | Validates lobby actions like joining and leaving. | Uses a 4-byte identifier to determine the action. Return logic is inverted. |
| `cm_IsCutsceneReady` | `0x1000d260` | 85% | High | Checks if a cutscene is ready to be played. | Iterates through players and checks their status. |
| `cm_Stub` | `0x1000d330` | 100% | High | Stub function that does nothing. | Placeholder for an unimplemented command. |
| `cm_NotYetImplemented` | `0x1000d340` | 100% | High | Stub function that does nothing. | Placeholder for an unimplemented command. |
| `cmdt_AllocClientPlayer` | `0x1000d570` | 85% | High | Command handler for allocating a new client player. | Calls `gm_AllocPlayer` to perform the allocation. |
| `cmdt_ChangePlayerIdentity` | `0x1000d6e0` | 90% | High | Command handler for changing a player's identity. | Calls `gm_ChangePlayerIdentity` to perform the change. |
| `cmdt_Free` | `0x1000d730` | 85% | High | Command handler for freeing a player or building. | Calls `gm_KillSpieler` or `gm_FreeBuilding`. |
| `cmdt_SellObjectEx` | `0x1000d930` | 75% | Medium | Command handler for selling an object with extended functionality. | Complex logic for handling various sale scenarios. |
| `cmdt_ClearStorageSlot` | `0x1000e690` | 85% | High | Command handler for clearing a storage slot. | Calls `handleRemoveObjectFromList`. |
| `cmdt_ChangePlayerDesire` | `0x1000e9c0` | 85% | High | Command handler for changing a player's desire. | Updates and clamps desire values. |
| `cm_ExchangeBits` | `0x1000eaa0` | 90% | High | Command handler for exchanging bits between players. | Updates player data based on size and offset. |
| `cm_ExchangeFloat` | `0x1000eb70` | 90% | High | Command handler for exchanging a float value between players. | Updates player data at a given offset. |
| `cm_AllocCharacter` | `0x1000f980` | 85% | High | Command handler for allocating a new character. | Calls `gm_AllocPlayer` to create a new character. |
| `cm_StartCutscene` | `0x1000ff60` | 85% | High | Command handler for starting a cutscene. | Calls `cm_IsCutsceneReady` and sets player flags. |
| `cm_ZombieCommand` | `0x10010260` | 95% | High | Command handler for zombie-related commands. | Dispatches to sub-handlers based on a command ID. |
| `cm_AllocGraveyardWorker` | `0x10010310` | 90% | High | Command handler for allocating a graveyard worker. | Calls `handleAllocGraveyardWorker2`. |
| `cm_GetPlayerAmtId` | `0x10010350` | 90% | High | Command handler for getting a player's "Amt" ID. | Calls `handleGetPlayerAmtId`. |
| `srv_HandlePlayerCommand` | `0x10010390` | 80% | Medium | Command handler for player-related commands. | Dispatches to sub-handlers based on a command ID. |
| `cm_ExGetBuildingDataSize` | `0x100104a0` | 90% | High | Command handler for getting the size of a building's data. | Returns the size of a building's data structure. |
| `cm_ExValidateBuildingData` | `0x10010530` | 90% | High | Command handler for validating a building's data. | Validates specific fields within a building's data structure. |
| `cm_ExGetBuildingDataPtr` | `0x100105b0` | 90% | High | Command handler for getting a pointer to a building's data. | Returns a pointer to the requested data. |
| `cm_ExIterateBuildingData` | `0x10010710` | 85% | High | Command handler for iterating over a building's data. | Iterates through building data and calls a callback. |
| `cm_ExAllocGraveyard` | `0x10010850` | 80% | Medium | Command handler for allocating a graveyard. | Allocates and initializes a graveyard building. |
| `cm_ExAllocGraveyardField` | `0x100109d0` | 80% | Medium | Command handler for allocating a graveyard field. | Allocates and initializes a graveyard field within a building. |
| `cmdt_AllocClientPlayer` | `0x1000d570` | 85% | High | Command handler for allocating a new client player. | Calls `gm_AllocPlayer` to perform the allocation. |
| `cmdt_ChangePlayerIdentity` | `0x1000d6e0` | 90% | High | Command handler for changing a player's identity. | Calls `gm_ChangePlayerIdentity` to perform the change. |
| `cmdt_Free` | `0x1000d730` | 85% | High | Command handler for freeing a player or building. | Calls `gm_KillSpieler` or `gm_FreeBuilding`. |
| `cmdt_SellObjectEx` | `0x1000d930` | 75% | Medium | Command handler for selling an object with extended functionality. | Complex logic for handling various sale scenarios. |
| `cmdt_ClearStorageSlot` | `0x1000e690` | 85% | High | Command handler for clearing a storage slot. | Calls `handleRemoveObjectFromList`. |
| `cmdt_ChangePlayerDesire` | `0x1000e9c0` | 85% | High | Command handler for changing a player's desire. | Updates and clamps desire values. |
| `cm_ExchangeBits` | `0x1000eaa0` | 90% | High | Command handler for exchanging bits between players. | Updates player data based on size and offset. |
| `cm_ExchangeFloat` | `0x1000eb70` | 90% | High | Command handler for exchanging a float value between players. | Updates player data at a given offset. |
| `cm_AllocCharacter` | `0x1000f980` | 85% | High | Command handler for allocating a new character. | Calls `gm_AllocPlayer` to create a new character. |
| `cm_StartCutscene` | `0x1000ff60` | 85% | High | Command handler for starting a cutscene. | Calls `cm_IsCutsceneReady` and sets player flags. |
| `cm_ZombieCommand` | `0x10010260` | 95% | High | Command handler for zombie-related commands. | Dispatches to sub-handlers based on a command ID. |
| `cm_AllocGraveyardWorker` | `0x10010310` | 90% | High | Command handler for allocating a graveyard worker. | Calls `handleAllocGraveyardWorker2`. |
| `cm_GetPlayerAmtId` | `0x10010350` | 90% | High | Command handler for getting a player's "Amt" ID. | Calls `handleGetPlayerAmtId`. |
| `srv_HandlePlayerCommand` | `0x10010390` | 80% | Medium | Command handler for player-related commands. | Dispatches to sub-handlers based on a command ID. |
| `cm_ExGetBuildingDataSize` | `0x100104a0` | 90% | High | Command handler for getting the size of a building's data. | Returns the size of a building's data structure. |
| `cm_ExValidateBuildingData` | `0x10010530` | 90% | High | Command handler for validating a building's data. | Validates specific fields within a building's data structure. |
| `cm_ExGetBuildingDataPtr` | `0x100105b0` | 90% | High | Command handler for getting a pointer to a building's data. | Returns a pointer to the requested data. |
| `cm_ExIterateBuildingData` | `0x10010710` | 85% | High | Command handler for iterating over a building's data. | Iterates through building data and calls a callback. |
| `cm_ExAllocGraveyard` | `0x10010850` | 80% | Medium | Command handler for allocating a graveyard. | Allocates and initializes a graveyard building. |
| `cm_ExAllocGraveyardField` | `0x100109d0` | 80% | Medium | Command handler for allocating a graveyard field. | Allocates and initializes a graveyard field within a building. |
