**LINKEDLIST**
is a linear collection of data elements, called nodes, where each node points to the next node in the sequence.  Unlike arrays, linked lists don't store elements in contiguous memory locations, allowing for dynamic resizing and efficient insertions/deletions.  Each node in a linked list typically contains data and a pointer (or link) to the next node. This C++ code defines and demonstrates three fundamental linked list data structures: singly linked lists, doubly linked lists, and circular linked lists. 
**1. Includes and Namespace:**

```c++
#include <iostream>
using namespace std;
```

*   `#include <iostream>`: This line includes the iostream library, which provides input and output functionalities (like `cout` for printing to the console).
*   `using namespace std;`: This line brings the standard namespace into the current scope, so you don't have to write `std::` before elements like `cout` and `endl`.

**2. Node Structures:**

```c++
struct SinglyNode {
    int data;
    SinglyNode* next;
};

struct DoublyNode {
    int data;
    DoublyNode* next;
    DoublyNode* prev;
};
```

*   `SinglyNode`: This structure defines a node for a singly linked list. It contains an integer `data` and a pointer `next` to the next node in the list.
*   `DoublyNode`: This structure defines a node for a doubly linked list. It contains an integer `data`, a pointer `next` to the next node, and a pointer `prev` to the previous node.

**3. Singly Linked List Functions:**

```c++
void insertSingly(SinglyNode*& head, int data) {
    SinglyNode* newNode = new SinglyNode{data, nullptr}; // Create a new node
    if (!head) { // If the list is empty
        head = newNode;
    } else { // If the list is not empty
        SinglyNode* temp = head;
        while (temp->next) { // Traverse to the end of the list
            temp = temp->next;
        }
        temp->next = newNode; // Add the new node at the end
    }
}

void displaySingly(SinglyNode* head) {
    while (head) { // Traverse the list
        cout << head->data << " -> ";
        head = head->next;
    }
    cout << "NULL" << endl; // Print NULL to indicate the end of the list
}
```

*   `insertSingly`: Inserts a new node with the given `data` at the end of the singly linked list.
*   `displaySingly`: Prints the elements of the singly linked list to the console.

**4. Doubly Linked List Functions:**

```c++
void insertDoubly(DoublyNode*& head, int data) {
    DoublyNode* newNode = new DoublyNode{data, nullptr, nullptr}; // Create a new node
    if (!head) { // If the list is empty
        head = newNode;
    } else { // If the list is not empty
        DoublyNode* temp = head;
        while (temp->next) { // Traverse to the end of the list
            temp = temp->next;
        }
        temp->next = newNode; // Add the new node at the end
        newNode->prev = temp; // Set the previous pointer of the new node
    }
}

void displayDoubly(DoublyNode* head) {
    while (head) { // Traverse the list
        cout << head->data << " <-> ";
        head = head->next;
    }
    cout << "NULL" << endl; // Print NULL to indicate the end of the list
}
```

*   `insertDoubly`: Inserts a new node with the given `data` at the end of the doubly linked list.  It also correctly sets the `prev` pointer.
*   `displayDoubly`: Prints the elements of the doubly linked list.

**5. Circular Linked List Functions:**

```c++
void insertCircular(SinglyNode*& head, int data) {
    SinglyNode* newNode = new SinglyNode{data, nullptr}; // Create a new node
    if (!head) { // If the list is empty
        head = newNode;
        newNode->next = head; // Make it circular (point to itself)
    } else { // If the list is not empty
        SinglyNode* temp = head;
        while (temp->next != head) { // Traverse until you reach the head again
            temp = temp->next;
        }
        temp->next = newNode; // Add the new node at the end
        newNode->next = head; // Make the last node point to the head
    }
}

void displayCircular(SinglyNode* head) {
    if (!head) return; // If the list is empty, return

    SinglyNode* temp = head;
    do { // Traverse the list
        cout << temp->data << " -> ";
        temp = temp->next;
    } while (temp != head); // Stop when you reach the head again
    cout << " (Back to Head)" << endl; // Indicate that it's a circular list
}
```

*   `insertCircular`: Inserts a new node into the circular linked list.
*   `displayCircular`: Prints the elements of the circular linked list.

**6. `main` Function:**

```c++
int main() {
    // Singly Linked List
    SinglyNode* singlyHead = nullptr; // Initialize an empty singly linked list
    insertSingly(singlyHead, 10);
    insertSingly(singlyHead, 20);
    insertSingly(singlyHead, 30);
    cout << "Singly Linked List: ";
    displaySingly(singlyHead);

    // Doubly Linked List
    DoublyNode* doublyHead = nullptr; // Initialize an empty doubly linked list
    insertDoubly(doublyHead, 100);
    insertDoubly(doublyHead, 200);
    insertDoubly(doublyHead, 300);
    cout << "Doubly Linked List: ";
    displayDoubly(doublyHead);

    // Circular Linked List
    SinglyNode* circularHead = nullptr; // Initialize an empty circular linked list
    insertCircular(circularHead, 1);
    insertCircular(circularHead, 2);
    insertCircular(circularHead, 3);
    cout << "Circular Linked List: ";
    displayCircular(circularHead);

    return 0;
}
```

*   The `main` function demonstrates the usage of the linked list functions. It creates instances of each type of linked list, inserts some data, and then displays the contents of each list.

**Output:**

```
Singly Linked List: 10 -> 20 -> 30 -> NULL
Doubly Linked List: 100 <-> 200 <-> 300 <-> NULL
Circular Linked List: 1 -> 2 -> 3 ->  (Back to Head)
```

**Explanation of the Output:**

*   The output shows the contents of each linked list after the insertions.
*   The singly linked list contains 10, 20, and 30.
*   The doubly linked list contains 100, 200, and 300.
*   The circular linked list contains 1, 2, and 3, and the "(Back to Head)" indicates the circular connection.


