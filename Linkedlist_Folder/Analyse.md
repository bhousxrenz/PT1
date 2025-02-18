Let's break down this C++ code, which demonstrates singly linked lists, doubly linked lists, and circular linked lists.

**Explanation of Linked Lists:**

A linked list is a dynamic data structure where elements (nodes) are connected through pointers. Unlike arrays, linked lists don't store elements in contiguous memory locations.  This makes them flexible for insertions and deletions, but accessing elements can be slower.

*   **Singly Linked List:** Each node has data and a pointer (`next`) to the next node.  Traversal is unidirectional.

*   **Doubly Linked List:** Each node has data, a pointer to the next node (`next`), and a pointer to the previous node (`prev`). This allows bidirectional traversal.

*   **Circular Linked List:** The last node's `next` pointer points back to the head, creating a cycle.

**Code Breakdown:**

1.  **Node Structures:**
    *   `SinglyNode`: Represents a node in a singly linked list.
    *   `DoublyNode`: Represents a node in a doubly linked list.

2.  **Singly Linked List Functions:**
    *   `insertSingly(SinglyNode*& head, int data)`: Inserts a new node containing `data` at the *end* of the list.
    *   `displaySingly(SinglyNode* head)`: Prints the data of each node, followed by "-> ", and then "NULL" at the end.

3.  **Doubly Linked List Functions:**
    *   `insertDoubly(DoublyNode*& head, int data)`: Inserts a new node at the *end* of the list.  Crucially, it also sets the `prev` pointer of the new node and the `next` pointer of the previous node.
    *   `displayDoubly(DoublyNode* head)`: Prints the data of each node, followed by " <-> ", and then "NULL".

4.  **Circular Linked List Functions:**
    *   `insertCircular(SinglyNode*& head, int data)`: Inserts a new node at the *end* of the list. The `next` pointer of the last node is made to point back to the head, creating the circular link.
    *   `displayCircular(SinglyNode* head)`: Prints the data of each node. Because it's circular, the loop continues until the head is encountered again. It prints " (Back to Head)" to signify the completion of the circle.

5.  **`main()` Function:**
    *   Creates empty linked lists of each type.
    *   Inserts data into each list.
    *   Calls the respective display functions to print the contents of each list.

**Predicted Output:**

```
Singly Linked List: 10 -> 20 -> 30 -> NULL
Doubly Linked List: 100 <-> 200 <-> 300 <-> NULL
Circular Linked List: 1 -> 2 -> 3 ->  (Back to Head)
```
