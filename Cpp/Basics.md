# Basics

<https://roadmap.sh/cpp>

```cpp
#include <iostream>

int main() {
    int number;
    std::cout << "Enter an integer: ";
    std::cin >> number;
    std::cout << "You entered: " << number << std::endl;
    return 0;
}
```

## Control Structures

### If-Else

```cpp
if (condition) {
    // Code to execute if the condition is true
} else {
    // Code to execute if the condition is false
}
```

### For

```cpp
for (initialization; condition; update) {
    // Code to execute while the condition is true
}
```

### While

```cpp
while (condition) {
    // Code to execute while the condition is true
}
```

### Do-While

```cpp
do {
    // block of code to execute
} while (condition);
```

### Switch

```cpp
switch (variable) {
    case value1:
        // Code to execute if variable == value1
        break;
    case value2:
        // Code to execute if variable == value2
        break;
    // More cases...
    default:
        // Code to execute if variable does not match any case value
}
```

## Operators

- Addition: `int sum = a + b;`
- Subtraction: `int difference = a - b;`
- Multiplication: `int product = a * b;`
- Division: `float quotient = float(a) / float(b);`
- Modulus: `int remainder = a % b;`
- Increment: `int z = x++;`
- Decrement: `int z = x--;`
- And: `(expression1 && expression2)`
- Or: `(expression1 || expression2)`
- Not: `!(expression)`
- Bitwise AND: `int result = 5 & 3;`
- Bitwise OR: `int result = 5 | 3;`
- Bitwise XOR: `int result = 5 ^ 3;`
- Bitwise NOT: `int result = ~5;`
- Bitwise Left Shift: `int result = 5 << 1;`
- Bitwise Right Shift: `int result = 5 >> 1;`

## Code Splitting

### Header Files (.h or .hpp)

Header files, usually with the `.h` or `.hpp` extension, are responsible for declaring classes, functions, and variables that are needed by multiple source files.
They act as an interface between different parts of the code, making it easier to manage dependencies and reduce the chances of duplicated code.

```cpp
// example.h
#ifndef EXAMPLE_H
#define EXAMPLE_H

class Example {
public:
    void printMessage();
};

#endif
```

### Source Files (.cpp)

Source files, with the `.cpp` extension, are responsible for implementing the actual functionality defined in the corresponding header files.
They include the header files as needed and provide the function and class method definitions.

```cpp
// example.cpp
#include "example.h"
#include <iostream>

void Example::printMessage() {
    std::cout << "Hello, code splitting!" << std::endl;
}
```

### Separate Compilation

C++ allows for separate compilation, which means that each source file can be compiled independently into an object file.
These object files can then be linked together to form the final executable.
This provides faster build times when making changes to a single source file since only that file needs to be recompiled, and the other object files can be reused.

```sh
# Compile each source file into an object file
g++ -c main.cpp -o main.o
g++ -c example.cpp -o example.o

# Link object files together to create the executable
g++ main.o example.o -o my_program
```
