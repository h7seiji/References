# Basics

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
