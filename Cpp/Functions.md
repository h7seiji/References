# Functions

```cpp
return_type function_name(parameter list) {
    // function body
}
```

## Function Prototypes

In some cases, you might want to use a function before actually defining it. To do this, you need to declare a function prototype at the beginning of your code.

A function prototype is a declaration of the function without its body, and it informs the compiler about the function’s name, return type, and parameters.

```cpp
#include <iostream>

// Function prototype
int multiplyNumbers(int x, int y);

int main() {
    int num1 = 3, num2 = 7;
    int result = multiplyNumbers(num1, num2); // Calling the function
    std::cout << "The product is: " << result << std::endl;
    return 0;
}

// Function definition
int multiplyNumbers(int x, int y) {
    int product = x * y;
    return product;
}
```

## Lambda Functions

Here is a basic syntax of a lambda function in C++:

```cpp
[capture-list](parameters) -> return_type {
    // function body
};
```

- capture-list: A list of variables from the surrounding scope that the lambda function can access.
- parameters: The list of input parameters, just like in a regular function. Optional.
- return_type: The type of the value that the lambda function will return. This part is optional, and the compiler can deduce it in many cases.
- function body: The code that defines the operation of the lambda function.

### capture-by-value

```cpp
int multiplier = 3;
auto times = [multiplier](int a) {
    return a * multiplier;
};
int result = times(5); // result = 15
```

### capture-by-reference

```cpp
int expiresInDays = 45;
auto updateDays = [&expiresInDays](int newDays) {
    expiresInDays = newDays;
};
updateDays(30); // expiresInDays = 30
```

Note that, when using the capture by reference, any change made to the captured variable inside the lambda function will affect its value in the surrounding scope.
