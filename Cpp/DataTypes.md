# Data Types

## Fundamental Data Types

### Integer (int)

Integers are whole numbers that can store both positive and negative values. The size of int depends on the system architecture (usually 4 bytes).

```cpp
int num = 42;
```

There are variants of int that can hold different ranges of numbers:

- short (`short int`): Smaller range than int.
- long (`long int`): Larger range than int.
- long long (`long long int`): Even larger range than long int.

### Floating-Point (float, double)

- float: Provides single-precision floating-point numbers. It typically occupies 4 bytes of memory.

```cpp
float pi = 3.14f;
```

- double: Provides double-precision floating-point numbers. It consumes more memory (usually 8 bytes) but has a higher precision than float.

```cpp
double pi_high_precision = 3.1415926535;
```

### Character (char)

Characters represent a single character, such as a letter, digit, or symbol. They are stored using the ASCII value of the symbol and typically occupy 1 byte of memory.

```cpp
char letter = 'A';
```

### Boolean (bool)

Booleans represent logical values: true or false. They usually occupy 1 byte of memory.

```cpp
bool is_cpp_great = true;
```

## Derived Data Types

### Arrays

Arrays are used to store multiple values of the same data type in consecutive memory locations.

```cpp
int numbers[5] = {1, 2, 3, 4, 5};
```

### Pointers

Pointers are used to store the memory address of a variable.

```cpp
int num = 42;
int* pNum = &num;
```

### References

References are an alternative way to share memory locations between variables, allowing you to create an alias for another variable.

```cpp
int num = 42;
int& numRef = num;
```

## User-Defined Data Types

### Structures (struct)

Structures are used to store different data types under a single variable and accessibility of member variables and methods are public.

```cpp
struct Person {
    std::string name;
    int age;
    float height;
};

Person p1 = {"John Doe", 30, 5.9};
```

### Classes (class)

Classes are similar to structures, but the accessibility of the member data and function are governed by access specifiers. By default access to members of a class is private.

```cpp
class Person {
public:
    std::string name;
    int age;

    void printInfo() {
        std::cout << "Name: " << name << ", Age: " << age << std::endl;
    };
};

Person p1;
p1.name = "John Doe";
p1.age = 30;
```

### Unions (union)

Unions are used to store different data types in the same memory location.

```cpp
union Data {
    int num;
    char letter;
    float decimal;
};

Data myData;
myData.num = 42;
```

## Static Typing

n C++, static typing means that the data type of a variable is determined at compile time, before the program is executed. This means that a variable can only be used with data of a specific type, and the compiler ensures that the operations performed with the variable are compatible with its type. If there is a mismatch , the compiler will adjust the data type of variable to match another provided it’s feasible . This process is known as Type Conversion. If compiler not able to achieve type conversion , Invalid Type Conversion error will be raised during compilation of the code .

C++ is a statically typed language, which means that it uses static typing to determine data types and perform type checking during compile time. This helps with ensuring type safety and can prevent certain types of errors from occurring during the execution of the program.

## Dynamic Typing in C++

C++ is known as a statically-typed language, which means the data types of its variables are determined at compile time. However, C++ also provides concepts to have certain level of dynamic typing, which means determining the data types of variables at runtime.

### `void*` Pointers

A void* pointer is a generic pointer that can point to objects of any data type. They can be used to store a reference to any type of object without knowing the specific type of the object.

```cpp
#include <iostream>

int main() {
    int x = 42;
    float y = 3.14f;
    std::string z = "Hello, world!";

    void* void_ptr;

    void_ptr = &x;
    std::cout << "int value: " << *(static_cast<int*>(void_ptr)) << std::endl;

    void_ptr = &y;
    std::cout << "float value: " << *(static_cast<float*>(void_ptr)) << std::endl;

    void_ptr = &z;
    std::cout << "string value: " << *(static_cast<std::string*>(void_ptr)) << std::endl;

    return 0;
}
```

### `std::any` (C++17)

C++17 introduced the std::any class which represents a generalized type-safe container for single values of any type.

```cpp
#include <iostream>
#include <any>

int main() {
    std::any any_value;

    any_value = 42;
    std::cout << "int value: " << std::any_cast<int>(any_value) << std::endl;

    any_value = 3.14;
    std::cout << "double value: " << std::any_cast<double>(any_value) << std::endl;

    any_value = std::string("Hello, world!");
    std::cout << "string value: " << std::any_cast<std::string>(any_value) << std::endl;

    return 0;
}
```

## Run-Time Type Identification (RTTI)

Run-Time Type Identification (RTTI) is a feature in C++ that allows you to obtain the type information of an object during program execution. This can be useful when using dynamic typing, where the type of an object can change at runtime.

There are two main mechanisms for RTTI in C++:

- `typeid` operator
- `dynamic_cast` operator
