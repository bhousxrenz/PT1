QUEUES a linear data structure that follows the First-In, First-Out (FIFO) principle, meaning the first element added is the first one removed.  Think of it like a line of people waiting – the person at the front is the first one served.  Queues are used in various applications, such as managing print jobs, handling requests in a web server, and implementing breadth-first search algorithms. a linear data structure that follows the First-In, First-Out (FIFO) principle, meaning the first element added is the first one removed.  Think of it like a line of people waiting – the person at the front is the first one served.  Queues are used in various applications, such as managing print jobs, handling requests in a web server, and implementing breadth-first search algorithms.

**1. Header and Namespace:**

```cpp
#include <iostream>
using namespace std;
```

*   `#include <iostream>`: Includes the iostream library for input/output operations (like `cout`).
*   `using namespace std;`: Uses the standard namespace to avoid writing `std::` before standard elements like `cout`.

**2. Macro Definition:**

```cpp
#define SIZE 5
```

*   `#define SIZE 5`: Defines a constant `SIZE` with a value of 5. This determines the maximum number of elements the circular queue can hold.  Using a macro is a common way to define constants in C++.

**3. CircularQueue Class:**

```cpp
class CircularQueue {
private:
    int items[SIZE], front, rear;
public:
    // ... (methods)
};
```

*   `class CircularQueue`: Declares a class named `CircularQueue` to represent the circular queue data structure.
*   `private:`: The members declared after this are only accessible within the class itself.
    *   `int items[SIZE]`: An integer array named `items` of size `SIZE` to store the queue elements.
    *   `int front`: An integer to keep track of the index of the front element in the queue.
    *   `int rear`: An integer to keep track of the index of the rear element in the queue.
*   `public:`: The members declared after this are accessible from outside the class.

**4. Constructor:**

```cpp
CircularQueue() {
    front = -1;
    rear = -1;
}
```

*   `CircularQueue()`: The constructor of the class. It initializes `front` and `rear` to -1, indicating that the queue is initially empty.

**5. `isFull()` Method:**

```cpp
bool isFull() {
    return (rear + 1) % SIZE == front;
}
```

*   `bool isFull()`: Returns `true` if the queue is full, `false` otherwise. The modulo operator (`%`) is crucial for implementing the circular behavior. The condition `(rear + 1) % SIZE == front` checks if the next position after `rear` (wrapping around the array if necessary) is equal to `front`.  If it is, the queue is full.

**6. `isEmpty()` Method:**

```cpp
bool isEmpty() {
    return front == -1;
}
```

*   `bool isEmpty()`: Returns `true` if the queue is empty, `false` otherwise.  A queue is empty if `front` is -1.

**7. `enqueue()` Method:**

```cpp
void enqueue(int value) {
    if (isFull()) {
        cout << "Queue is full!\n";
        return;
    }
    if (front == -1) front = 0; // If queue was empty, set front to 0
    rear = (rear + 1) % SIZE; // Increment rear in a circular manner
    items[rear] = value; // Insert the value at the new rear position
}
```

*   `void enqueue(int value)`: Adds an element (`value`) to the rear of the queue.
    1.  Checks if the queue is full. If it is, prints a message and returns.
    2.  If the queue was initially empty (`front == -1`), sets `front` to 0.
    3.  Updates `rear` using the modulo operator to wrap around the array.
    4.  Inserts the `value` at the `rear` index in the `items` array.

**8. `dequeue()` Method:**

```cpp
void dequeue() {
    if (isEmpty()) {
        cout << "Queue is empty!\n";
        return;
    }
    cout << "Dequeued: " << items[front] << endl; // Output the dequeued element
    if (front == rear) front = rear = -1; // If only one element, reset front and rear
    else front = (front + 1) % SIZE; // Increment front in a circular manner
}
```

*   `void dequeue()`: Removes the element at the front of the queue.
    1.  Checks if the queue is empty. If it is, prints a message and returns.
    2.  Prints the value being dequeued.
    3.  If the queue had only one element (`front == rear`), resets both `front` and `rear` to -1.
    4.  Otherwise, increments `front` using the modulo operator.

**9. `display()` Method:**

```cpp
void display() {
    if (isEmpty()) {
        cout << "Queue is empty!\n";
        return;
    }
    cout << "Queue elements: ";
    int i = front;
    while (true) {
        cout << items[i] << " ";
        if (i == rear) break;
        i = (i + 1) % SIZE;
    }
    cout << endl;
}
```

*   `void display()`: Displays the elements in the queue.
    1.  Checks if the queue is empty. If it is, prints a message and returns.
    2.  Iterates through the queue elements starting from `front` until `rear` is reached, using the modulo operator to handle the circular wrapping.

**10. `main()` Function:**

```cpp
int main() {
    CircularQueue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50); // Queue is now full
    q.display();
    q.dequeue(); // Dequeues 10
    q.enqueue(60); // 60 will be enqueued due to circularity
    q.display();
    return 0;
}
```

*   `int main()`: The main function where the program execution begins.
    1.  Creates a `CircularQueue` object `q`.
    2.  Enqueues elements 10, 20, 30, 40, and 50. The queue is now full.
    3.  Calls `display()` to print the queue elements.
    4.  Dequeues one element (10).
    5.  Enqueues 60. Because of the circular nature, 60 will be inserted at the position previously occupied by 10.
    6.  Calls `display()` again to show the updated queue.

**Output:**

```
Queue elements: 10 20 30 40 50 
Dequeued: 10
Queue elements: 60 20 30 40 50 
```

**Explanation of the Output:**

1.  The first `display()` call shows the queue is full with elements 10, 20, 30, 40, and 50.
2.  After dequeuing 10, the queue has space.
3.  When 60 is enqueued, it takes the "freed up" spot at the beginning of the array (due to the circular nature), so the queue becomes 60, 20, 30, 40, 50.
