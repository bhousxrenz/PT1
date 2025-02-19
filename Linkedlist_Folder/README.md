LINKEDLIST
is a linear collection of data elements, called nodes, where each node points to the next node in the sequence.  Unlike arrays, linked lists don't store elements in contiguous memory locations, allowing for dynamic resizing and efficient insertions/deletions.  Each node in a linked list typically contains data and a pointer (or link) to the next node.This C++ code defines and demonstrates the use of three fundamental data structures: singly linked lists, doubly linked lists, and circular linked lists. Let's break down the code section by section:

1. Node Structures:

SinglyNode: Represents a node in a singly linked list. It contains an integer data and a pointer next to the next node in the sequence.
DoublyNode: Represents a node in a doubly linked list. It contains an integer data, a pointer next to the next node, and a pointer prev to the previous node.
Circular Linked List Node: The code reuses the SinglyNode structure for the circular linked list, as a circular list can be implemented using just the next pointer.
2. Singly Linked List Functions:

insertSingly(SinglyNode*& head, int data): Inserts a new node with the given data at the end of the singly linked list. It handles the case where the list is empty (head == nullptr).
displaySingly(SinglyNode* head): Traverses the singly linked list and prints the data of each node, followed by "->", and finally "NULL" to indicate the end of the list.
3. Doubly Linked List Functions:

insertDoubly(DoublyNode*& head, int data): Inserts a new node with the given data at the end of the doubly linked list. It also correctly sets the prev pointer of the new node and the next pointer of the previous last node. Handles the empty list case.
displayDoubly(DoublyNode* head): Traverses the doubly linked list and prints the data of each node, followed by "<->", and "NULL" at the end.
4. Circular Linked List Functions:

insertCircular(SinglyNode*& head, int data): Inserts a new node with the given data at the end of the circular linked list. The key difference is that the next pointer of the last node is made to point back to the head to create the circular connection. Handles the empty list case (where the new node points to itself).
displayCircular(SinglyNode* head): Traverses the circular linked list and prints the data of each node, followed by "->". The traversal stops when the temp pointer reaches the head again, completing the circle. It adds "(Back to Head)" to the end of the output for clarity.
5. main Function:

Creates three linked lists: singlyHead (singly linked), doublyHead (doubly linked), and circularHead (circular linked).
Inserts some sample data into each list.
Calls the respective display functions to print the contents of each list to the console.
Output of the Code:
Singly Linked List: 10 -> 20 -> 30 -> NULL
Doubly Linked List: 100 <-> 200 <-> 300 <-> NULL
Circular Linked List: 1 -> 2 -> 3 ->  (Back to Head)

Explanation of the Output:
The singly linked list contains the elements 10, 20, and 30 in that order.
The doubly linked list contains the elements 100, 200, and 300.
The circular linked list contains the elements 1, 2, and 3, and the output indicates that it's circular by showing "(Back to Head)".
