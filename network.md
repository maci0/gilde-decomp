# `server.dll` Network Protocol

This document outlines the network protocol used by `server.dll` for communication between the server and clients.

## Packet Structure

All packets share a common header:

| Offset | Type      | Name      | Description                     |
|--------|-----------|-----------|---------------------------------|
| 0x0    | `uint8_t` | packet_id | The identifier for the packet.  |
| 0x1    | `uint8_t` | size      | The total size of the packet.   |

The server reads the `packet_id` and a `size` field to determine the total length of the incoming command, then reads that many bytes from the socket.

---

## Client → Server Packets

These packets are sent from the client to the server to trigger actions and game state changes.

### **`0x0A`**: `CMD_ALLOC_BUILDING`

Allocates a new building.

**Handler:** `cm_ExAllocGebaeude` (0x1000d350)

| Offset | Type       | Name          | Description                      |
|--------|------------|---------------|----------------------------------|
| 0x0    | `uint8_t`  | `packet_id`   | `0x0A`                           |
| 0x1    | `uint8_t`  | `size`        | `0x70` (112)                     |
| 0x2    | `uint16_t` | `building_id` | The ID of the building to create.|
| 0x4    | `uint32_t` | `player_id`   | The ID of the owner.             |
| 0x8    | `uint8_t[104]` | `padding`     | Unused.                          |

### **`0x0C`**: `CMD_ALLOC_PLAYER`

Allocates a new player character.

**Handler:** `cm_ExAllocSpieler` (0x1000d570)

| Offset | Type       | Name          | Description                      |
|--------|------------|---------------|----------------------------------|
| 0x0    | `uint8_t`  | `packet_id`   | `0x0C`                           |
| 0x1    | `uint8_t`  | `size`        | `0x70` (112)                     |
| 0x2    | `uint16_t` | `player_id`   | The ID of the player to create.  |
| 0x4    | `uint32_t` | `father_id`   | The ID of the player's father.   |
| 0x8    | `uint32_t` | `mother_id`   | The ID of the player's mother.   |
| 0xC    | `uint16_t` | `player_data` | Pointer to player data.          |
| 0xE    | `uint32_t` | `building_id` | The ID of the associated building.|
| 0x12   | `uint8_t`  | `gender`      | The gender of the player.        |
| 0x13   | `uint8_t`  | `age`         | The age of the player.           |
| 0x14   | `uint8_t`  | `init_type`   | The initialization type.         |
| 0x15   | `uint8_t[99]` | `padding`     | Unused.                          |

### **`0x11`**: `CMD_SELL_OBJECT`

Sells an object from one container to another.

**Handler:** `cm_ExSellObjekt` (0x1000d930)

| Offset | Type       | Name            | Description                           |
|--------|------------|-----------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id`     | `0x11`                                |
| 0x1    | `uint8_t`  | `size`          | `0x70` (112)                          |
| 0x2    | `uint32_t` | `seller_id`     | The ID of the selling container.      |
| 0x6    | `uint32_t` | `buyer_id`      | The ID of the buying container.       |
| 0xA    | `uint16_t` | `object_id`     | The ID of the object to sell.         |
| 0xC    | `uint32_t` | `count`         | The number of objects to sell.        |
| 0x10   | `uint8_t[100]`| `padding`       | Unused.                               |

### **`0x10`**: `CMD_MOVE_OBJECT`

Moves an object from one container to another.

**Handler:** `move_object` (0x1000d8a0)

| Offset | Type       | Name            | Description                           |
|--------|------------|-----------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id`     | `0x10`                                |
| 0x1    | `uint8_t`  | `size`          | `0x70` (112)                          |
| 0x2    | `uint32_t` | `source_id`     | The ID of the source container.       |
| 0x6    | `uint32_t` | `destination_id`| The ID of the destination container.  |
| 0xA    | `uint16_t` | `object_id`     | The ID of the object to move.         |
| 0xC    | `uint32_t` | `count`         | The number of objects to move.        |
| 0x10   | `uint8_t[100]`| `padding`       | Unused.                               |

### **`0x12`**: `CMD_PRODUCE_OBJECT`

Produces an object in a building.

**Handler:** `cm_ExProdObjekt` (0x1000e140)

| Offset | Type       | Name          | Description                           |
|--------|------------|---------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id`   | `0x12`                                |
| 0x1    | `uint8_t`  | `size`        | `0x70` (112)                          |
| 0x2    | `uint32_t` | `building_id` | The ID of the building.               |
| 0x6    | `uint16_t` | `object_id`   | The ID of the object to produce.      |
| 0x8    | `uint32_t` | `count`       | The number of objects to produce.     |
| 0xC    | `uint8_t[104]`| `padding`     | Unused.                               |

### **`0x4C`**: `CMD_CREATE_BUILDING`

Creates a new building.

**Handler:** `cm_CreateBuilding` (0x1000fb30)

| Offset | Type       | Name            | Description                           |
|--------|------------|-----------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id`     | `0x4C`                                |
| 0x1    | `uint8_t`  | `size`          | `0x70` (112)                          |
| 0x2    | `uint32_t` | `player_id`     | The ID of the player creating the building. |
| 0x6    | `uint8_t`  | `building_type` | The type of building to create.       |
| 0x7    | `uint8_t[107]`| `padding`       | Unused.                               |

### **`0x3D`**: `CMD_EMPLOY_WORKER`

Employs a worker in a building.

**Handler:** `cm_EmployWorker` (0x1000f730)

| Offset | Type       | Name          | Description                           |
|--------|------------|---------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id`   | `0x3D`                                |
| 0x1    | `uint8_t`  | `size`        | `0x70` (112)                          |
| 0x2    | `uint32_t` | `building_id` | The ID of the building.               |
| 0x6    | `uint32_t` | `worker_id`   | The ID of the worker to employ.       |
| 0xA    | `uint8_t[104]`| `padding`     | Unused.                               |

### **`0x21`**: `CMD_KILL_PLAYER`

Kills a player character.

**Handler:** `cm_KillPlayer` (0x1000f030)

| Offset | Type       | Name           | Description                           |
|--------|------------|----------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id`    | `0x21`                                |
| 0x1    | `uint8_t`  | `size`         | `0x70` (112)                          |
| 0x2    | `uint32_t` | `player_id`    | The ID of the player to kill.         |
| 0x6    | `uint32_t` | `cleanup_type` | The type of cleanup to perform.       |
| 0xA    | `uint8_t[104]`| `padding`      | Unused.                               |

### **`0x5A`**: `CMD_SET_PLAYER_MONEY`

Sets a player's money.

**Handler:** `cm_SetPlayerMoney` (0x1000ffc0)

| Offset | Type       | Name        | Description                           |
|--------|------------|-------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id` | `0x5A`                                |
| 0x1    | `uint8_t`  | `size`      | `0x70` (112)                          |
| 0x2    | `uint32_t` | `player_id` | The ID of the player.                 |
| 0x6    | `uint32_t` | `money`     | The amount of money to set.           |
| 0xA    | `uint8_t[104]`| `padding`   | Unused.                               |

### **`0x5B`**: `CMD_SET_PLAYER_TITLE`

Sets a player's title.

**Handler:** `cm_SetPlayerTitle` (0x10010010)

| Offset | Type       | Name        | Description                           |
|--------|------------|-------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id` | `0x5B`                                |
| 0x1    | `uint8_t`  | `size`      | `0x70` (112)                          |
| 0x2    | `uint32_t` | `player_id` | The ID of the player.                 |
| 0x6    | `uint8_t`  | `title`     | The title to set.                     |
| 0x7    | `uint8_t[107]`| `padding`   | Unused.                               |

### **`0x5D`**: `CMD_SET_PLAYER_SKILL`

Sets a player's skill.

**Handler:** `cm_SetPlayerSkill` (0x100100a0)

| Offset | Type       | Name        | Description                           |
|--------|------------|-------------|---------------------------------------|
| 0x0    | `uint8_t`  | `packet_id` | `0x5D`                                |
| 0x1    | `uint8_t`  | `size`      | `0x70` (112)                          |
| 0x2    | `uint32_t` | `player_id` | The ID of the player.                 |
| 0x6    | `uint8_t`  | `skill`     | The skill to set.                     |
| 0x7    | `uint8_t`  | `value`     | The value to set the skill to.        |
| 0x8    | `uint8_t[106]`| `padding`   | Unused.                               |

---

## Server → Client Packets

These packets are sent from the server to the client to provide information and game state updates.

### **`0x02`**: `CMD_INVALID_COMMAND`

Indicates that the last command sent by the client was invalid.

| Offset | Type      | Name        | Description      |
|--------|-----------|-------------|------------------|
| 0x0    | `uint8_t` | `packet_id` | `0x02`           |
| 0x1    | `uint8_t` | `size`      | `0x02` (2)       |

### **`0x04`**: `CMD_SET_PLAYER_ID`

Assigns a player ID to the client.

| Offset | Type       | Name        | Description      |
|--------|------------|-------------|------------------|
| 0x0    | `uint8_t`  | `packet_id` | `0x04`           |
| 0x1    | `uint8_t`  | `size`      | `0x06` (6)       |
| 0x2    | `uint32_t` | `player_id` | The player ID.   |

### **`0x08`**: `CMD_GAME_DATA_START`

Signals the start of game data transmission.

| Offset | Type      | Name        | Description      |
|--------|-----------|-------------|------------------|
| 0x0    | `uint8_t` | `packet_id` | `0x08`           |
| 0x1    | `uint8_t` | `size`      | `0x02` (2)       |

### **`0x09`**: `CMD_GAME_DATA_CHUNK`

A chunk of game data.

| Offset | Type        | Name        | Description          |
|--------|-------------|-------------|----------------------|
| 0x0    | `uint8_t`   | `packet_id` | `0x09`               |
| 0x1    | `uint8_t`   | `size`      | Variable             |
| 0x2    | `uint8_t[]` | `data`      | The game data chunk. |

### **`0x1E`**: `CMD_UPDATE_CITIZEN_AGE`

Updates the age of a citizen.

| Offset | Type       | Name         | Description      |
|--------|------------|--------------|------------------|
| 0x0    | `uint8_t`  | `packet_id`  | `0x1E`           |
| 0x1    | `uint8_t`  | `size`       | `0x0E` (14)      |
| 0x2    | `uint32_t` | `citizen_id` | The citizen ID.  |
| 0x6    | `uint32_t` | `days`       | Days to add.     |
| 0xA    | `uint32_t` | `months`     | Months to add.   |
| 0xE    | `uint32_t` | `years`      | Years to add.    |

### **`0x20`**: `CMD_SET_GAME_YEAR`

Sets the current game year.

| Offset | Type       | Name        | Description      |
|--------|------------|-------------|------------------|
| 0x0    | `uint8_t`  | `packet_id` | `0x20`           |
| 0x1    | `uint8_t`  | `size`      | `0x06` (6)       |
| 0x2    | `uint32_t` | `year`      | The game year.   |