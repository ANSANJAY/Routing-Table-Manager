# Inter-Process Communication for Networking Systems

This repository provides an in-depth exploration of leveraging **IPC methods** in C, specifically tailored for Linux-oriented applications. It sheds light on the management and iterative refinement of two pivotal networking structures, with an emphasis on synchronization and real-world applications.

## **Contents**

1. [Route Directory Structure](#route-directory-structure)
2. [MAC Archive Overview](#mac-archive-overview)
3. [Command Interface](#command-interface)
    - [Route Directory Management](#route-directory-management)
    - [MAC Archive Operations](#mac-archive-operations)
4. [Data Sync Protocols](#data-sync-protocols)
5. [Problem Overview](#problem-overview)
6. 

## Route Directory Structure

A standard entry in the routing directory comprises:
- `destination`: Denoting the target network's IPv4 address.
- `subnet_mask`: Numeric value (0-32) indicating the subnet mask.
- `gateway`: IPv4 address of the gateway.
- `out_interface`: Label of the egress interface.

## MAC Archive Overview

Each record in the MAC Archive has:
- `address_MAC`: Unique 6-byte Layer-2 MAC address identifier.

## Command Interface

### Route Directory Management
- `ADD destination subnet_mask gateway out_interface`: Inserts a novel route record.
- `MODIFY destination subnet_mask [new_gateway] [new_out_interface]`: Updates a matching route entry.
- `REMOVE destination subnet_mask`: Deletes the corresponding route record.

### MAC Archive Operations
- `ADD address_MAC`: Introduces a MAC entry and links an IP in shared memory.
- `REMOVE address_MAC`: Deletes a MAC entry and its shared memory counterpart.

## Data Sync Protocols

- **Initialization**: New clients receive complete state info for both directories upon connection.
- **Mirroring**: Legitimate server-side changes are reflected in client tables.
- **Termination Protocols**: Graceful shutdown procedures for both servers and clients.
- **Record Identification**: Ensures unique identification and management of entries.
- **Purging Protocols**: Provides mechanisms for clearing and refreshing directories.

## Problem Overview

```
+------------------+          +------------------+            +------------------------+
|     CLIENT       |          |      SERVER      |            |    SHARED MEMORY       |
|------------------|          |------------------|            |------------------------|
| - Synchronizes data        | - Manages Routing Table       | - Holds mapping of MAC  |
|   with the Server          |   and MAC List                |   Addresses to IP       |
| - Receives updates         | - Updates the client about    | - Data accessible by    |
|   on changes to the        |   changes via Unix Domain     |   clients               |
|   Routing Table and        |   Sockets                     | - Facilitates quick     |
|   MAC List                 | - Processes CRUD operations   |   lookups               |
| - Makes lookups in         |   on the tables               |                         |
|   shared memory            | - Can flush data & inform     |                         |
|   for MAC -> IP mapping    |   clients                     |                         |
+------------------+          +------------------+            +------------------------+
          |                          |                             |
          '-------- Unix Domain -----+---------------- Shared ------'
                   Sockets                                 Memory


```

