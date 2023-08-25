# Doubly Linked List (DLL) Implementation - `dll.c`

This file contains the implementation for a doubly linked list (DLL). A DLL is a type of linked list in which each node contains a data part and two pointers. The two pointers point to the next and the previous node in the sequence, respectively.

## Functions

### 1. `dll_t *init_dll()`
Initializes an empty DLL.

- **Return**: A pointer to the initialized list.

#### How it works:
- Allocates memory for a new DLL structure and a dummy node.
- This dummy node acts as a sentinel node; both the head and tail pointers of the DLL point to this node in an empty list.
- Returns the DLL structure.

### 2. `void append(dll_t *dll, void *data)`
Appends a new node with the given data at the end of the list.

- **Parameters**:
  - `dll`: Pointer to the doubly linked list.
  - `data`: Generic pointer to data to be stored in the new node.

#### How it works:
- Allocates memory for a new DLL node.
- Sets the data of this node to the provided data.
- Adjusts the `next` and `prev` pointers to place this node at the end of the list.
- If there is an error in the process (e.g., the head changes), a message is printed to the console. *(Note: This part seems to be a debug message that might not be necessary in a production environment.)*

### 3. `void del(dll_t *dll, dll_node_t *node)`
Deletes a specified node from the list.

- **Parameters**:
  - `dll`: Pointer to the doubly linked list.
  - `node`: Pointer to the node to be deleted.

#### How it works:
- Updates the `next` pointer of the node preceding the node-to-be-deleted to point to the node following the node-to-be-deleted.
- Updates the `prev` pointer of the node following the node-to-be-deleted to point to the node preceding the node-to-be-deleted.
- If the node-to-be-deleted is the tail node, updates the DLL's tail pointer to point to the previous node.
- Frees the memory allocated to the node-to-be-deleted.

### 4. `void deinit_dll(dll_t *dll)`
Deletes all nodes from the list and frees the memory allocated to the DLL structure.

- **Parameters**:
  - `dll`: Pointer to the doubly linked list.

#### How it works:
- Iterates through each node in the list (starting from the node after the head) and deletes it.
- Once all nodes are deleted, frees the memory allocated to the DLL structure.

---

**Note**: The provided code makes use of `calloc` for memory allocation. This function not only allocates the required memory but also sets it to zero. This ensures that the memory is clean when it is first accessed.

---

Developed by Anamika.
