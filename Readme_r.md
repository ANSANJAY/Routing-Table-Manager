# Data Synchronization Using Unix Domain Sockets 🌐🔗

## Overview 📖

Achieve data synchronization between processes running on the same machine using IPC. Our project leverages Unix domain sockets to ensure consistent communication and synchronization between processes.

## Features 🚀

### 1. **Routing Table Manager (RTM)** 📡
- 🖥 Manages the L3 routing table.
- 📤 Sends notifications of any changes.
- ✅ Ensures consistent table state across all connected clients.

### 2. **Client-Server Model** 🔄
- **RTM Process (Server)**: Manages the routing table.
- **Client Processes**: Receive updates from the server and sync their local data accordingly.

### 3. **CRUD Operations** 🛠
- **C** (Create): Add a new entry 🆕.
- **U** (Update): Modify an existing entry ✏️.
- **D** (Delete): Remove an entry 🗑.

### 4. **Admin Dashboard** 👩‍💼👨‍💼
Allows the admin to interact directly with the RTM process for table management.

## Data Structures & Formats 📄

- **Operation Codes**: Create, Update, Delete.
- **Routing Table Entry**: Includes destination, gateway, and interface.
- **Notification Message**: Operation code + related data.

## Getting Started 🚀

1. Clone this repo `git clone https://github.com/ANSANJAY/Routing-Table-Manager.git`.
2. Navigate to the project directory `cd project-directory`.
3. Run `make` to build the project.
4. Execute the main program `./main`.

## License 📜

This project is licensed under the MIT License. See `LICENSE` for more information.

---

Developed with 💖 by `Anamika`
