STACK is a linear data structure that follows the Last-In, First-Out (LIFO) principle, meaning the last element added is the first one 1  removed.  Imagine a stack of plates – you can only take the top plate off, and the last plate you put on is the first one you take off. Stacks are used in various applications, such as function call management in programming, expression evaluation, and undo/redo mechanisms in software. This C++ code demonstrates several applications of the `std::stack` container, including string reversal, balanced parenthesis checking, basic stack operations, and decimal-to-binary conversion.

**1. Includes and Namespace:**

```c++
#include <iostream>
#include <stack>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;
```

*   `#include <iostream>`: For input/output operations (e.g., `cout`).
*   `#include <stack>`: For using the `std::stack` container.
*   `#include <vector>`: Although not directly used, it's included, potentially for future use or was left over from previous iterations of the code.
*   `#include <string>`: For string manipulation.
*   `#include <algorithm>`: For the `std::reverse` function (although the code implements string reversal manually using a stack, this include is not needed for the current code).
*   `using namespace std;`: To avoid writing `std::` before standard library elements.

**2. `reverseString()` Function:**

```c++
string reverseString(string str) {
    stack<char> s;
    for (char c : str) {
        s.push(c);
    }
    string reversedStr = "";
    while (!s.empty()) {
        reversedStr += s.top();
        s.pop();
    }
    return reversedStr;
}
```

*   Takes a string `str` as input.
*   Creates an empty stack of characters `s`.
*   Iterates through the input string `str`, pushing each character onto the stack.
*   Creates an empty string `reversedStr`.
*   While the stack is not empty, pops the top element from the stack and appends it to `reversedStr`.
*   Returns the `reversedStr`.

**3. `isBalanced()` Function:**

```c++
bool isBalanced(string str) {
    stack<char> s;
    for (char c : str) {
        if (c == '(' || c == '{' || c == '[') {
            s.push(c);
        } else if (c == ')' || c == '}' || c == ']') {
            if (s.empty()) {
                return false; // Unmatched closing parenthesis
            }
            char top = s.top();
            s.pop();
            if ((c == ')' && top != '(') || (c == '}' && top != '{') || (c == ']' && top != '[')) {
                return false; // Mismatched parentheses
            }
        }
    }
    return s.empty(); // All parentheses should be matched
}
```

*   Takes a string `str` containing parentheses as input.
*   Uses a stack to track opening parentheses.
*   If an opening parenthesis is encountered, it's pushed onto the stack.
*   If a closing parenthesis is encountered:
    *   Checks if the stack is empty (if so, it's an unmatched closing parenthesis, so return `false`).
    *   Pops the top element from the stack.
    *   Checks if the popped element matches the closing parenthesis (if not, it's a mismatch, so return `false`).
*   Finally, returns `true` if the stack is empty (all parentheses are matched), and `false` otherwise.

**4. `main()` Function:**

```c++
int main() {
    // 1. String Reversal
    string str = "Hello, Stack!";
    string reversed = reverseString(str);
    cout << "Reversed string: " << reversed << endl; // Output: !kcatS ,olleH

    // 2. Balanced Parentheses Check
    string balancedStr = "{[()]}";
    string unbalancedStr = "{[(])}";
    cout << "Balanced string check: " << isBalanced(balancedStr) << endl;    // Output: 1 (true)
    cout << "Unbalanced string check: " << isBalanced(unbalancedStr) << endl; // Output: 0 (false)

    // 3. Stack Operations (Demonstration)
    stack<int> myStack;
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    cout << "\nStack operations:" << endl;
    cout << "Top element: " << myStack.top() << endl; // Output: 30
    cout << "Stack size: " << myStack.size() << endl;    // Output: 3
    myStack.pop();
    cout << "Top element after pop: " << myStack.top() << endl; // Output: 20
    cout << "Is stack empty? " << myStack.empty() << endl; // Output: 0 (false)

    // 4. Converting Decimal to Binary using Stack:
    int decimalNum = 25;
    stack<int> binaryStack;

    while (decimalNum > 0) {
        binaryStack.push(decimalNum % 2);
        decimalNum /= 2;
    }

    cout << "\nBinary representation of 25: ";
    while (!binaryStack.empty()) {
        cout << binaryStack.top();
        binaryStack.pop();
    }
    cout << endl; // Output: 11001

    return 0;
}
```

*   The `main()` function demonstrates the usage of the `reverseString()`, `isBalanced()`, and basic stack operations.
*   It reverses the string "Hello, Stack!".
*   Checks if "{[()]}" is balanced (true) and "{[(])}" is unbalanced (false).
*   Demonstrates `push()`, `top()`, `size()`, and `pop()` methods of the stack.
*   Finally, it converts the decimal number 25 to its binary representation using a stack.

**Output:**

```
Reversed string: !kcatS ,olleH
Balanced string check: 1
Unbalanced string check: 0

Stack operations:
Top element: 30
Stack size: 3
Top element after pop: 20
Is stack empty? 0

Binary representation of 25: 11001
```

