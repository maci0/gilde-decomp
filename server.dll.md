# `server.dll` Architecture Report

This document provides a detailed architectural overview of the `server.dll` module from *Europa 1400: Gold Edition*. Its purpose is to document the server's design and behavior, including its core components, subsystems, and data management strategies.

## Table of Contents

- [1. Core Architecture](#1-core-architecture)
  - [1.1. Server Lifecycle](#11-server-lifecycle)
  - [1.2. Threading Model](#12-threading-model)
  - [1.3. Main Game Loop](#13-main-game-loop)
- [2. Subsystems](#2-subsystems)
  - [2.1. Networking](#21-networking)
  - [2.2. Memory Management](#22-memory-management)
  - [2.3. VFS and File I/O](#23-vfs-and-file-io)
  - [2.4. Error Handling and Crash Reporting](#24-error-handling-and-crash-reporting)
- [3. Game State Synchronization](#3-game-state-synchronization)
- [4. Data Storage](#4-data-storage)
  - [4.1. Global Data Structures](#41-global-data-structures)
  - [4.2. Game Data Files](#42-game-data-files)

## 1. Core Architecture

The `server.dll` module is a multithreaded, single-instance game server for *Europa 1400: Gold Edition*. It is designed to manage the complete lifecycle of a multiplayer game session, from initialization and player management to game state synchronization and final shutdown. The server operates on a client-server model where one client is designated as the "serving host," with the authority to load the initial game state.

### 1.1. Server Lifecycle

The server's lifecycle is managed through a sequence of initialization, execution, and shutdown steps:

```
+----------------+      +------------------+      +------------------+      +----------------+
|   `Init`       |----->| `srv_GameLoop`   |----->| `srv_InitServer` |----->|   Main Loop    |
| (Export)       |      | (Thread Start)   |      | (Initialization) |      | (Active)       |
+----------------+      +------------------+      +------------------+      +----------------+
        ^
        |
+----------------+      +------------------+      +------------------+
|   `Exit`       |<-----|  (Shutdown)      |<-----| (Cleanup)        |
| (Export)       |      | `g_bShutdownFlag`|      |                  |
+----------------+      +------------------+      +------------------+
```

### 1.2. Threading Model

The server uses a simple multithreading model with two primary threads:

-   **Main Thread**: The thread that loads the `server.dll` library. It is responsible for calling the `Init` and `Exit` functions to start and stop the server.
-   **Game Loop Thread**: A dedicated thread, created by `Init`, that runs the `srv_GameLoop` function. This design isolates the main server logic from the main thread, preventing the game from freezing if the server performs blocking operations.

### 1.3. Main Game Loop

The core of the server is the `srv_GameLoop`, which continuously processes game logic and network events. The loop's behavior is conditional, based on the game state (e.g., lobby vs. active game).

```
+------------------------------------+
| `srv_GameLoop`                     |
+------------------------------------+
|                                    |
|  +----------------------------+    |
|  | `srv_InitServer`           |    |
|  +----------------------------+    |
|                                    |
|  WHILE `!g_bShutdownFlag`          |
|  |                                  |
|  |  +-------------------------+   |
|  |  | `srv_AcceptClient`      |   |
|  |  +-------------------------+   |
|  |                                  |
|  |  +-------------------------+   |
|  |  | `srv_ProcessClientCmds` |   |
|  |  +-------------------------+   |
|  |                                  |
|  |  IF `is_game_active()`     |   |
|  |  |                           |   |
|  |  |  +--------------------+ |   |
|  |  |  | `sim_Update`       | |   |
|  |  |  +--------------------+ |   |
|  |  |                           |   |
|  |  END_IF                    |   |
|  |                                  |
|  |  +-------------------------+   |
|  |  | `Sleep(1)`              |   |
|  |  +-------------------------+   |
|  |                                  |
|  END_WHILE                         |
|                                    |
+------------------------------------+
```

## 2. Subsystems

### 2.1. Networking

The networking subsystem uses a non-blocking TCP model with Winsock. It queues incoming and outgoing commands to avoid blocking the main game loop.

-   **Command Queuing**: Incoming commands are placed in a queue by `srv_RecvFromClient` and processed by `srv_ProcessClientCommands`. Outgoing commands are queued with `enqueue_client_command` and sent by `srv_SendQueuedCommands`.
-   **Command Dispatch**: `srv_DispatchGameCommand` uses a jump table to map command IDs to their corresponding `cm_*` handler functions, allowing for efficient command processing.

```
+-----------------+   +----------------------+   +-----------------------+   +-------------------+
| Client Action   |-->| `srv_RecvFromClient` |-->| `enqueue_client_cmd`  |-->| Command Queue     |
+-----------------+   +----------------------+   +-----------------------+   +-------------------+
                                                                                    |
                                                                                    v
+-----------------+   +----------------------+   +-----------------------+   +-------------------+
| Server Response |<--| `srv_SendData`       |<--| `cm_*` Handler        |<--| `srv_DispatchCmd` |
+-----------------+   +----------------------+   +-----------------------+   +-------------------+
```

### 2.2. Memory Management

The server uses a custom memory pool allocator to manage memory for game objects, which is more efficient than standard dynamic allocation.

-   **`m_alloc_init`**: Initializes the memory manager.
-   **`m_pool_alloc`**: Allocates a fixed-size block from a pre-allocated pool.
-   **`m_pool_free`**: Returns a block to the pool.

This system is designed to minimize memory fragmentation and reduce the overhead of frequent allocations and deallocations.

```
+------------------------------------+
| Memory Pool                        |
+------------------------------------+
|                                    |
|  +-----------+  +-----------+      |
|  | Free Block|  | Used Block| ...  |
|  +-----------+  +-----------+      |
|                                    |
+------------------------------------+
```

### 2.3. VFS and File I/O

The server uses a virtual file system (VFS) to manage access to game data files. This system supports reading from compressed archives, using the statically linked `zlib` library for decompression.

-   **`vfs_open`**: Opens a file from the VFS, handling both compressed and uncompressed data.
-   **`file_read`**: Reads data from a file, performing decompression and CRC32 checks as needed.

```
+----------------+   +----------------+   +----------------+   +----------------+
| `vfs_open`     |-->| `file_read`    |-->| `zlib_inflate` |-->|   Game Data    |
+----------------+   +----------------+   +----------------+   +----------------+
```

### 2.4. Error Handling and Crash Reporting

The server includes a robust error handling system to ensure stability.

-   **`unhandledExceptionHandler`**: A top-level exception filter that catches unhandled exceptions.
-   **`writeArchiveFile`**: Generates a crash dump file containing the exception context and memory state, which is crucial for debugging.

```
+------------------+   +---------------------+   +--------------------+
| Exception        |-->| `unhandledExFilter` |-->| `writeArchiveFile` |
+------------------+   +---------------------+   +--------------------+
```

## 3. Game State Synchronization

Game state synchronization is a critical process that occurs when a game is loaded. The "serving host" is responsible for providing the initial game state, which is then broadcast to all other clients.

1.  The serving host sends the game state to the server.
2.  The server receives the data and uses `srv_LoadGameState` to process it.
3.  `srv_LoadGameState` calls a series of `handleLoad*` functions to deserialize the data.
4.  `ls_ID2Ptr` is called to perform "pointer fix-ups," converting object IDs into direct memory pointers, which is essential for re-establishing object relationships.

```
+--------------+    +---------------------+    +-----------------------+    +-------------------+
| Serving Host |-->| `srv_LoadGameState` |-->| `handleLoad*` funcs   |-->| `ls_ID2Ptr`       |
| (Client)     |    | (Server)            |    | (Deserialization)     |    | (Pointer Fix-up)  |
+--------------+    +---------------------+    +-----------------------+    +-------------------+
```

## 4. Data Storage

### 4.1. Global Data Structures

The game state is stored in a collection of global data structures that are initialized at startup and modified during gameplay. Key structures include:

-   **`g_client_slots`**: An array of structures representing connected clients.
-   **`g_player_data`**: An array storing data for all players in the game.
-   **`g_building_data`**: An array for all buildings.
-   **`g_object_data`**: An array for all game objects.

### 4.2. Game Data Files

The server loads initial game data from several files:

-   **`game.ini`**: Contains server configuration settings.
-   **`aemter.dat`**: Contains data for the "Amt" (office/rank) system.
