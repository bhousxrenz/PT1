## Analysis of the C++ Linked List Code

This code implements a singly linked list in C++ with several common operations: insertion at the beginning, insertion at the end, deletion of a node, reversal of the list, and display of the list. Let's break down the code section by section:

**1. Node Structure:**

```cpp
struct Node {
    int data;
    Node* next;
};
```

This defines the structure of a node in the linked list. Each node contains an integer `data` and a pointer `next` to the next node in the list.

**2. Insertion at the Beginning:**

```cpp
void insertAtBeginning(Node*& head, int data) {
    Node* newNode = new Node{data, head};
    head = newNode;
}
```

This function inserts a new node with the given `data` at the beginning of the list. It creates a new node, sets its `next` pointer to the current head, and then updates the head to point to the new node.

**3. Insertion at the End:**

```cpp
void insertAtEnd(Node*& head, int data) {
    Node* newNode = new Node{data, nullptr};
    if (!head) {
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next) temp = temp->next;
    temp->next = newNode;
}
```

This function inserts a new node at the end of the list. It first checks if the list is empty. If it is, the new node becomes the head. Otherwise, it traverses the list to the end and then appends the new node.

**4. Deletion of a Node:**

```cpp
void deleteNode(Node*& head, int key) {
    if (!head) return;
    if (head->data == key) {
        Node* temp = head;
        head = head->next;
        delete temp;
        return;
    }
    Node* temp = head;
    while (temp->next && temp->next->data != key) temp = temp->next;
    if (temp->next) {
        Node* toDelete = temp->next;
        temp->next = temp->next->next;
        delete toDelete;
    }
}
```

This function deletes the node with the given `key` from the list. It handles the case where the node to be deleted is the head. Otherwise, it traverses the list to find the node before the node to be deleted and then updates the `next` pointer to bypass the node to be deleted.

**5. Reversal of the List:**

```cpp
void reverseList(Node*& head) {
    Node* prev = nullptr, *curr = head, *next = nullptr;
    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    head = prev;
}
```

This function reverses the linked list iteratively. It uses three pointers: `prev`, `curr`, and `next` to reverse the links between the nodes.

**6. Display of the List:**

```cpp
void display(Node* head) {
    while (head) {
        cout << head->data << " -> ";
        head = head->next;
    }
    cout << "NULL\n";
}
```

This function traverses the list and prints the data of each node.

**7. Main Function:**

The `main` function demonstrates the usage of the linked list operations. It creates a linked list, inserts elements, deletes an element, reverses the list, and displays the list at various stages.

## Predicted Output:

```
Linked List: 1 -> 5 -> 10 -> 20 -> 30 -> NULL
After deleting 20: 1 -> 5 -> 10 -> 30 -> NULL
Reversed List: 30 -> 10 -> 5 -> 1 -> NULL
```
