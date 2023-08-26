### client.c: An Overview

This file  define the operations of a client in a client-server model. Its primary role is to communicate with a server over UNIX domain sockets and synchronize its copy of certain network data structures like routing tables and MAC lists.

---

### Header Files:

- Standard Libraries: These are common libraries used for various purposes. Examples include:
  - `stdio.h` for input-output operations.
  - `stdlib.h` and `string.h` for string manipulations and memory management.
  - `sys/*` are system-specific libraries for inter-process communication, file operations, etc.
  - `signal.h` for handling signals (like keyboard interrupts).
- Custom Headers: Include files like `dll.h`, `mac-list.h`, `routing-table.h`, and `sync.h` which provide specific functionality or define structures related to the networking context of the application.

---

### Global Variables:

- `int data_socket`: A socket descriptor for communication with the server.
- `int loop`: A flag indicating if the client should continue running.
- `int disconnect`: A flag that tells the server the client wishes to disconnect.
- `dll_t *routing_table`: A pointer to a doubly linked list representing the routing table.
- `dll_t *mac_list`: A pointer to another list representing the MAC address list.

---

### Functions:

1. **signal_handler(int signal_num)**:
    - This function is called when specific signals are received by the process. Signals are a way to notify processes of specific events.
    - `SIGINT`: When the user sends an interrupt (e.g., pressing Ctrl+C), this code disconnects from the server, deallocates memory, and exits.
    - `SIGUSR1`: When this signal is received, it reinitializes the routing table and MAC list.

2. **display_ds(int synchronized)**:
    - This function allows the user to view the contents of the synchronized routing table or MAC list. The user is prompted to see the list, and depending on their choice, the relevant list is displayed.

---

### Main Function: `int main()`

1. **Initialization**:
    - The routing table and MAC list are initialized.
    - A UNIX domain socket is created for communication. This socket is specific to UNIX-like operating systems and allows processes on the same machine to communicate.
    - Connection to the server is established using the socket. If the server isn't running, the client informs the user and exits.

2. **Communication**:
    - The client sends its process id to the server.
    - Signal handlers are registered to ensure graceful handling of interruptions.
    - The client then enters an infinite loop, where it continuously waits for updates from the server.
        - The `sync_msg` received indicates the kind of update (whether for L3 - IP routing table or L2 - MAC address list) and the exact update details.
        - The client then processes this message using `process_sync_mesg()`, which updates the relevant list accordingly.
        - The `display_ds` function is called, giving the user an option to view the updated list.

3. **Exiting**:
    - If the client breaks out of the loop (e.g., through a signal or server disconnection), the program ends.

---

In simpler terms: 
Think of this client as someone constantly on the phone with a server, asking for updates on lists that keep track of various networking details. Whenever the server has something new to share (like a new IP address or a MAC address change), the client takes note, updates its records, and can show them to the user if asked. If the user decides to hang up the phone (by pressing Ctrl+C or other means), the client gracefully ends the call, tidies up its notes, and stops running.
