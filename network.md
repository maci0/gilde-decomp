# `server.dll` Network Protocol

This document outlines the network protocol used by `server.dll` for communication between the server and clients.

## Packet Structure

The basic packet structure is as follows:

| Field | Type | Description |
|---|---|---|
| Packet ID | `uint8_t` | The identifier for the packet type. |
| Payload | `uint8_t[]` | The data associated with the packet. |

## Server -> Client Packets

| Packet ID | Name | Description |
|---|---|---|
| `0x02` | `CMD_INVALID_COMMAND` | Indicates that the last command sent by the client was invalid. |
| `0x04` | `CMD_SET_PLAYER_ID` | Assigns a player ID to the client. |
| `0x08` | `CMD_GAME_DATA_START` | Signals the start of game data transmission. |
| `0x09` | `CMD_GAME_DATA_CHUNK` | A chunk of game data. |
| `0x1E` | `CMD_UPDATE_CITIZEN_AGE` | Updates the age of a citizen. |
| `0x20` | `CMD_SET_GAME_YEAR` | Sets the current game year. |

## Client -> Server Packets

| Packet ID | Name | Description |
|---|---|---|
| `0x01` | `CMD_ALLOC_BUILDING` | Requests the allocation of a new building. |
| `0x02` | `CMD_ALLOC_PLAYER` | Requests the allocation of a new player. |
| `0x06` | `CMD_SELL_OBJECT` | Requests to sell an object. |
| `0x07` | `CMD_MOVE_OBJECT` | Requests to move an object. |
| `0x08` | `CMD_PRODUCE_OBJECT` | Requests to produce an object. |
| `0x0D` | `CMD_CREATE_BUILDING` | Requests to create a building. |
| `0x0E` | `CMD_EMPLOY_WORKER` | Requests to employ a worker. |
| `0x0F` | `CMD_KILL_PLAYER` | Requests to kill a player. |
| `0x11` | `CMD_SET_PLAYER_MONEY` | Requests to set a player's money. |
| `0x12` | `CMD_SET_PLAYER_TITLE` | Requests to set a player's title. |
| `0x13` | `CMD_SET_PLAYER_SKILL` | Requests to set a player's skill. |
| `0x1D` | `CMD_UPDATE_CITIZEN_AGE` | Requests to update a citizen's age. |
| `0x1E` | `CMD_SET_CITIZEN_DATA` | Requests to set a citizen's data. |
| `0x5F` | `CMD_LOBBY_GET_PLAYER_LIST` | Requests the list of players in the lobby. |
| `0x60` | `CMD_LOBBY_SET_PLAYER_READY` | Requests to set the player's ready status. |
| `0x61` | `CMD_LOBBY_JOIN_GAME` | Requests to join the game from the lobby. |

### `CMD_ALLOC_BUILDING` (0x01)

| Field | Type | Description |
|---|---|---|
| `building_type` | `uint8_t` | The type of building to allocate. |
| `owner_id` | `uint16_t` | The ID of the building's owner. |
| `unknown` | `uint8_t[108]` | Unknown data. |

### `CMD_ALLOC_PLAYER` (0x02)

| Field | Type | Description |
|---|---|---|
| `player_type` | `uint8_t` | The type of player to allocate. |
| `father_id` | `uint32_t` | The ID of the player's father. |
| `mother_id` | `uint32_t` | The ID of the player's mother. |
| `player_data` | `uint16_t` | Pointer to the player's data structure. |
| `building_data` | `uint32_t` | Pointer to the building data. |
| `gender` | `uint8_t` | The gender of the player. |
| `age` | `uint8_t` | The age of the player. |
| `init_type` | `uint8_t` | The initialization type. |
| `unknown` | `uint8_t[99]` | Unknown data. |

### `CMD_MOVE_OBJECT` (0x07)

| Field | Type | Description |
|---|---|---|
| `source_container_id` | `uint32_t` | The ID of the source container. |
| `destination_container_id` | `uint32_t` | The ID of the destination container. |
| `object_id` | `uint16_t` | The ID of the object to move. |
| `count` | `uint32_t` | The number of objects to move. |
| `unknown` | `uint8_t[100]` | Unknown data. |

### `CMD_SELL_OBJECT` (0x06)

| Field | Type | Description |
|---|---|---|
| `seller_id` | `uint32_t` | The ID of the seller. |
| `buyer_id` | `uint32_t` | The ID of the buyer. |
| `object_id` | `uint16_t` | The ID of the object to sell. |
| `count` | `uint32_t` | The number of objects to sell. |
| `unknown` | `uint8_t[100]` | Unknown data. |

### `CMD_PRODUCE_OBJECT` (0x08)

| Field | Type | Description |
|---|---|---|
| `building_id` | `uint32_t` | The ID of the building where the object is produced. |
| `object_id` | `uint16_t` | The ID of the object to produce. |
| `count` | `uint32_t` | The number of objects to produce. |
| `unknown` | `uint8_t[104]` | Unknown data. |

### `CMD_KILL_PLAYER` (0x0F)

| Field | Type | Description |
|---|---|---|
| `player_id` | `uint32_t` | The ID of the player to kill. |
| `cleanup_type` | `uint32_t` | The type of cleanup to perform. |
| `unknown` | `uint8_t[104]` | Unknown data. |

### `CMD_EMPLOY_WORKER` (0x0E)

| Field | Type | Description |
|---|---|---|
| `building_id` | `uint32_t` | The ID of the building where the worker is employed. |
| `worker_id` | `uint32_t` | The ID of the worker to employ. |
| `unknown` | `uint8_t[104]` | Unknown data. |

### `CMD_CREATE_BUILDING` (0x0D)

| Field | Type | Description |
|---|---|---|
| `player_id` | `uint32_t` | The ID of the player who is creating the building. |
| `building_type` | `uint8_t` | The type of building to create. |
| `unknown` | `uint8_t[107]` | Unknown data. |

### `CMD_SET_PLAYER_MONEY` (0x11)

| Field | Type | Description |
|---|---|---|
| `player_id` | `uint32_t` | The ID of the player. |
| `money` | `uint32_t` | The amount of money to set. |
| `unknown` | `uint8_t[104]` | Unknown data. |

### `CMD_SET_PLAYER_TITLE` (0x12)

| Field | Type | Description |
|---|---|---|
| `player_id` | `uint32_t` | The ID of the player. |
| `title` | `uint8_t` | The title to set. |
| `unknown` | `uint8_t[107]` | Unknown data. |

### `CMD_SET_PLAYER_SKILL` (0x13)

| Field | Type | Description |
|---|---|---|
| `player_id` | `uint32_t` | The ID of the player. |
| `skill` | `uint8_t` | The skill to set. |
| `value` | `uint8_t` | The value to set the skill to. |
| `unknown` | `uint8_t[106]` | Unknown data. |

### `CMD_UPDATE_CITIZEN_AGE` (0x1D)

| Field | Type | Description |
|---|---|---|
| `citizen_id` | `uint32_t` | The ID of the citizen to update. |
| `days` | `uint32_t` | The number of days to add to the citizen's age. |
| `months` | `uint32_t` | The number of months to add to the citizen's age. |
| `years` | `uint32_t` | The number of years to add to the citizen's age. |
| `unknown` | `uint8_t[92]` | Unknown data. |

### `CMD_SET_CITIZEN_DATA` (0x1E)

| Field | Type | Description |
|---|---|---|
| `citizen_id` | `uint32_t` | The ID of the citizen to update. |
| `gender` | `uint8_t` | The gender of the citizen. |
| `age` | `uint32_t` | The age of the citizen. |
| `birth_year` | `uint32_t` | The birth year of the citizen. |
| `unknown` | `uint8_t[95]` | Unknown data. |

### `CMD_LOBBY_GET_PLAYER_LIST` (0x5F)

| Field | Type | Description |
|---|---|---|
| `unknown` | `uint8_t[112]` | Unknown data. |

### `CMD_LOBBY_SET_PLAYER_READY` (0x60)

| Field | Type | Description |
|---|---|---|
| `player_id` | `uint32_t` | The ID of the player. |
| `ready_status` | `uint32_t` | The ready status of the player. |
| `unknown` | `uint8_t[104]` | Unknown data. |

### `CMD_LOBBY_JOIN_GAME` (0x61)

| Field | Type | Description |
|---|---|---|
| `player_id` | `uint32_t` | The ID of the player. |
| `unknown` | `uint8_t[108]` | Unknown data. |
