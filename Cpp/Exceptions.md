# Exception Handling

C++ provides a set of keywords and constructs for implementing exception handling:

- `try`: Defines a block of code that should be monitored for exceptions.
- `catch`: Specifies the type of exception to be caught and the block of code that shall be executed when that exception occurs.
- `throw`: Throws an exception that will be caught and handled by the appropriate catch block.
- `noexcept`: Specifies a function that doesn’t throw exceptions or terminates the program if an exception is thrown within its scope.

```cpp
#include <iostream>

int divide(int a, int b) {
    if (b == 0) {
        throw "Division by zero!";
    }
    return a / b;
}

int main() {
    int num1, num2;

    std::cout << "Enter two numbers for division: ";
    std::cin >> num1 >> num2;

    try {
        int result = divide(num1, num2);
        std::cout << "The result is: " << result << std::endl;
    } catch (const char* msg) {
        std::cerr << "Error: " << msg << std::endl;
    }

    return 0;
}
```

## Standard Exceptions

C++ provides a standard set of exception classes under the `<stdexcept>` library which can be used as the exception type for more specific error handling. Some of these classes include:

- `std::exception`: Base class for all standard exceptions.
- `std::logic_error`: Represents errors which can be detected statically by the program.
- `std::runtime_error`: Represents errors occurring during the execution of a program.

## Access Violations

An access violation is a specific type of error that occurs when a program attempts to access an illegal memory location. In C++, access violations are most commonly caused by:

- Dereferencing a null or invalid pointer.
- Accessing an array out of bounds.
- Reading or writing to memory freed by the user or the operating system.

## Exit Codes

Exit codes, also known as “return codes” or “status codes”, are numeric values that a program returns to the calling environment (usually the operating system) when it finishes execution.
These codes are used to indicate the success or failure of a program’s execution.

0 is the standard exit code for a successful execution, while non-zero exit codes typically indicate errors or other exceptional situations.
The actual meanings of non-zero exit codes can vary between different applications or systems.

In C++, you can return an exit code from the `main` function by using the `return` statement, or you can use the `exit()` function, which is part of the C++ Standard Library.
