# Routing Table Module

The `Routing-Table` directory in the repository holds the implementation and interface definition of a basic IP routing table. This table contains entries that are used to determine the next hop or exit interface (OIF) for a given destination IP.

## Files:

1. **routing-table.h**: This file provides the structure and function declarations related to the routing table.
2. **routing-table.c**: This file contains the implementations of the functions declared in `routing-table.h`.

---

### routing-table.h

This header file defines the core components and public interfaces for the routing table functionality. 

#### Constants:

- `IP_ADDR_LEN`: This constant defines the maximum length of an IP address string.
- `OIF_LEN`: This constant defines the maximum length of the "Outgoing Interface" (OIF) string.

#### Data Structures:

#### `routing_table_entry_t`

This data structure encapsulates the details of an individual route within the routing table.

- **`dest` (Destination IP address)**: Represents the IP address to which a particular packet should be forwarded. When a packet arrives, its destination IP address is checked against this value to determine the appropriate path.

- **`mask` (Subnet mask value)**: Often used in conjunction with the destination IP to determine a range of IP addresses. This allows a single routing entry to represent multiple possible IP addresses. By applying the mask to an incoming packet's IP, the router can decide if the packet belongs to a certain group of IPs and therefore which route it should take.

- **`gw` (Gateway IP)**: Indicates the next hop's IP address. If a packet matches the route's destination IP and mask, it will be forwarded to this gateway IP.

- **`oif` (Outgoing Interface)**: Signifies the interface (like eth0, eth1, etc.) on the router or device that will be used to forward the packet towards its destination.


#### Public APIs:

- `display_routing_table(const dll_t *routing_table)`: Function to display the entire routing table.
  
- `find_routing_table_entry(const dll_t *routing_table, const char *dest, const unsigned short mask)`: Looks up an entry in the routing table based on the destination IP and subnet mask.
  
- `update(dll_node_t *node, const char *gw, const char *oif)`: Update the gateway and OIF for a given routing table entry.

---

### routing-table.c
## Explaining the Logic in `routing-table.c`

### `display_routing_table` Function

This function is responsible for presenting the entries of the routing table to the user.

**Logic**:
1. The function begins by printing a statement, indicating that it's about to display the routing table.
2. It initializes a pointer `node` to point to the first node in the doubly linked list (DLL) representation of the routing table.
3. An iteration (a `while` loop) is initiated, which will continue until the pointer points back to the head of the DLL, signifying that all entries have been traversed.
4. For each node, the data (of type `routing_table_entry_t`) is fetched and its details (destination IP, mask, gateway, and OIF) are printed to the console.
5. After printing an entry's details, the pointer `node` is advanced to the next node in the list, and the iteration continues.

This function provides a sequential display of each routing table entry, offering a quick overview of the routing paths defined in the system.

### `find_routing_table_entry` Function

The purpose of this function is to locate a specific entry in the routing table based on given criteria (destination IP and subnet mask).

**Logic**:
1. The function starts with a pointer `node` set to the first node in the DLL representation of the routing table.
2. A `while` loop is used to traverse the list. The loop terminates if the pointer returns to the head of the DLL.
3. Within the loop, the function compares the destination IP and mask of each entry with the given values.
4. If a match is found, the loop is broken, and the `node` pointing to the matching entry is returned.
5. If no match is found after traversing the entire list, the function returns a pointer to the head of the list.

This search mechanism allows for quick lookups and modifications based on the destination IP and mask.

### `update` Function

This function serves to modify an existing entry's fields: the gateway and the Outgoing Interface (OIF).

**Logic**:
1. The function receives a pointer to a node (which represents a routing table entry) and the new values for the gateway and OIF.
2. Using `memset`, it clears (sets to zero) the current values of the gateway and OIF in the entry. This step ensures no remnants of old values interfere with the new ones.
3. Using `memcpy`, the function copies the new gateway and OIF values to the routing table entry. The lengths of the values to be copied are determined by the `strlen` of the input values.
4. The routing table entry is now updated with the new gateway and OIF values.

The `update` function ensures that the modification of an entry's details is done safely and accurately.

---

**Note**: The `Routing-Table` module relies on the doubly linked list (DLL) module for storing and manipulating the routing entries. The DLL module provides a generic implementation of a doubly linked list, making it reusable for various applications like the MAC List and the Routing Table.

