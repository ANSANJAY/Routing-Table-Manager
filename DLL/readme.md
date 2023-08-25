# Circular Doubly Linked List (DLL) Implementation

This repository provides an implementation of a generic circular doubly linked list. This data structure can hold any type of data due to its usage of void pointers. The implementation comprises three main files: `dll.c`, `dll.h`, and `main.c`.

## 1. `dll.h` - Header File

### Data Structures

- `dll_node_t`: Represents a node in the circular doubly linked list. It contains:
  - `data`: A void pointer to store any type of data.
  - `next`: Pointer to the next node.
  - `prev`: Pointer to the previous node.

- `dll_t`: Represents the circular doubly linked list itself. It contains:
  - `head`: Pointer to the dummy head node.
  - `tail`: Pointer to the last node in the list.

### Function Prototypes

- `dll_t *init_dll()`: Initializes and returns an empty list.
- `void append(dll_t *dll, void *data)`: Adds a new node with data to the back of the list.
- `void del(dll_t *dll, dll_node_t *node)`: Deletes a specified node from the list.
- `void deinit_dll(dll_t *dll)`: Deletes all nodes from the list and frees the memory.

## 2. `dll.c` - Implementation File

This file provides the implementations for the function prototypes declared in `dll.h`.

- The `init_dll` function initializes a circular DLL with a dummy head node, which acts as both the head and tail of the empty list.
- The `append` function allows adding a new node with data to the end of the list.
- The `del` function facilitates the removal of a specified node from the list, updating the head or tail pointers if necessary.
- The `deinit_dll` function clears all nodes from the list and frees the memory allocated to the list.

## 3. `main.c` - Test Program

This file contains a test suite to validate the functionalities of the DLL. It provides utility functions to search for a node, print the list in forward and reverse order, and a main driver function to simulate various operations.

### Utility Functions

- `dll_node_t *find(dll_t *dll, int n)`: Searches for a node with integer data in the DLL.
- `void print(dll_t *dll)`: Prints the contents of the DLL from head to tail.
- `void reverse_print(dll_t *dll)`: Prints the contents of the DLL from tail to head.

### Main Driver Function

The main function:
1. Initializes an empty DLL.
2. Inserts nodes with integers 0 to 4.
3. Demonstrates reverse printing of the list.
4. Validates the `find` function.
5. Performs deletions of specified nodes.
6. Prints the list post deletions in forward and reverse directions.
7. Deinitializes the DLL.
8. Exits the program.

## Compilation & Execution

To compile and run the test program:

```shell
gcc -o test_program dll.c main.c
./test_program
