## MAC-List

The MAC-List module provides functionality for managing a list of MAC addresses. The primary data structure used is a circular doubly linked list, borrowed from the `DLL` directory we explored earlier. This list helps manage and look up MAC address entries.

### Structure Definitions

**mac_list_entry_t**: 
This structure represents a single entry in the MAC list.

- **mac**: 
A character array storing the MAC address. MAC addresses are 17 characters long (e.g., `00:1A:2B:3C:4D:5E`) with an extra character for the null terminator, making the total length 18.

### API Overview

1. **display_mac_list**: 
This function takes in the MAC list and prints all the MAC addresses in it. It also fetches the corresponding IP address for each MAC entry by calling the `get_IP` function. This function prints a list of MAC to IP mappings.

2. **find_mac**: 
A utility function that searches for a MAC address in the MAC list and returns the node containing that MAC address, if found. If the MAC address is not in the list, it returns the head node.

### Dependencies

- **DLL**: 
The MAC list heavily relies on the functionality provided by the Doubly Linked List (DLL) module to manage the list. This dependency can be seen in the include directives and the use of types like `dll_t` and `dll_node_t`.

- **Routing-Table**: 
There seems to be a dependency on the Routing-Table module as there's an inclusion of its header and a reference to a function `get_IP` that presumably fetches the IP address corresponding to a MAC address.

### Sample Usage

The `display_mac_list` function provides a way to visualize the current state of the MAC list:

```c
dll_t *mac_list = init_dll(); // Initialize the DLL first

// Add entries to the list...

display_mac_list(mac_list); // This would print the MAC and corresponding IP addresses.


The find_mac function provides a lookup functionality:

dll_node_t *mac_node = find_mac(mac_list, "00:1A:2B:3C:4D:5E");

if(mac_node != mac_list->head) {
    // Found the MAC in the list
}
