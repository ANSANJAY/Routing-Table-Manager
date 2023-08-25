# Shared Memory & Data Synchronization Using Unix Domain Sockets 🌐🔗🔐

## Overview 📖

Achieve data synchronization between processes running on the same machine using IPC. Our project leverages both shared memory and Unix domain sockets to ensure consistent communication and synchronization between processes.

```sql
  +--------+       +------------+       +--------+
  | Client |<----->| Unix Domain|<----->| Server |
  +---|----+       |   Sockets  |       |---|----+
      |            +------------+           ^
      | Signal                             | Signal
      v            +------------+           v
      |            | Shared Mem |           |
  +---|----+       +------------+       +---|----+
  | Client |            ^                | Server |
  +--------+            |                | Process|
                        | Signal        +--------+
                        v
                   +------------+
                   | Data Sync  |
                   +------------+

```

## Features 🚀

### 1. **Routing Table Manager (RTM) with Signal Handling** 📡🚦
- 🖥 Manages the L3 routing table.
- 🧮 Incorporates an ARP (Address Resolution Protocol) table.
- 📤 Sends notifications of any changes.
- ✅ Ensures consistent table state across all connected clients.
- 📟 Uses signal handling to notify clients about major events like flushing tables.

```sql
+---------------------+
|      RTM TABLE      |
+---------------------+
|   Destination   |   Gateway   |   Interface   |
+-----------------|-------------|---------------|
|   192.168.1.0   |  10.0.0.1   |      eth0     |
+-----------------|-------------|---------------|
|   10.0.1.0      |  10.0.0.2   |      eth1     |
+-----------------|-------------|---------------|
|        ...      |     ...     |       ...     |
+-----------------|-------------|---------------|
```

```sql

+--------------------------------------------------+
|                  ARP TABLE      |
+--------------------------------------------------+
|   MAC Address     |   IP Address in Shared Mem  |
+-------------------|-----------------------------|
|  00:1A:2B:3C:4D:5E  |  192.168.1.10  [SHM_KEY_1]  |
+-------------------|-----------------------------|
|  11:22:33:44:55:66  |  10.0.1.20     [SHM_KEY_2]  |
+-------------------|-----------------------------|
|        ...        |           ...               |
+-------------------|-----------------------------|


```

### 2. **Client-Server Model with Shared Memory** 🔄🔐
- **RTM Process (Server)**: Manages both the routing table and ARP table.
- **Client Processes**: Receive updates through Unix domain sockets and retrieve relevant data from shared memory. Sends its own PID upon synchronization using UDS for future signal-based communications.

### 3. **CRUD Operations with Signal Integration** 🛠🚦
- **C** (Create): Add a new entry 🆕.
- **U** (Update): Modify an existing entry ✏️.
- **D** (Delete): Remove an entry 🗑.
- On certain operations, signals might be sent to the clients for real-time updates.

### 4. **Admin Dashboard with Extended Controls** 👩‍💼👨‍💼
- Allows admins to interact directly with the RTM process for routing table and ARP management.
- 🧑‍💻 Admins can insert MAC-IP pairs, and these entries are reflected in shared memory.
- Introduces controls to flush entire tables and propagate this event to all clients using signals.

### 5. **Data Structures, Memory Management & Signal Mechanisms** 💾🔑🚦
- **Shared Memory Keys**: MAC addresses function as the keys to access IP addresses in shared memory.
- **Operation Codes**: Create, Update, Delete actions for MAC addresses.
- **ARP Table Entry**: Features the MAC to IP mapping.
- **Notification Message**: Comprises the operation code along with MAC address data.
- **Signal Handling**: `SIGUSR1` for major notifications like flushing tables.

### 6. **Client Termination Protocol & Server Cleanup** 🛑✨
- Upon intending to disconnect, the client will clear its routing table and ARP table.
- A special "goodbye" message notifies the server, prompting the removal of the client's PID from the server's records.

## Getting Started 🚀

1. Clone this repo: `git clone https://github.com/ANSANJAY/Routing-Table-Manager.git`.
2. Navigate to the project directory: `cd project-directory`.
3. Build the project: `make`.
4. Execute the main program: `./main`.

## License 📜

This project is licensed under the GNU License. Kindly refer to the `LICENSE` file for detailed information.

---

Developed with 💖 by `Anamika`
