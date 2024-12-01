# Scope

Scope refers to the visibility and accessibility of variables, functions, classes, and other identifiers in a C++ program.
It determines the lifetime and extent of these identifiers.
In C++, there are four types of scope:

- Global scope
- Local scope
- Namespace scope
- Class scope

## Global scope

Identifiers declared outside any function or class have a global scope.
They can be accessed from any part of the program (unless hidden by a local identifier with the same name).
The lifetime of a global identifier is the entire duration of the program.

```cpp
#include <iostream>

int globalVar; // This is a global variable

int main() {
    std::cout << "Global variable: " << globalVar << std::endl;
}
```

## Local scope

Identifiers declared within a function or a block have a local scope.
They can be accessed only within the function or the block they were declared in.
Their lifetime is limited to the duration of the function/block execution.

```cpp
#include <iostream>

void localExample() {
    int localVar; // This is a local variable
    localVar = 5;
    std::cout << "Local variable: " << localVar << std::endl;
}

int main() {
    localExample();
    // std::cout << localVar << std::endl; //error: ‘localVar’ was not declared in this scope
}
```

## Namespace scope

A namespace is a named scope that groups related identifiers together.
Identifiers declared within a namespace have the namespace scope.
They can be accessed using the namespace name and the scope resolution operator `::`.

```cpp
#include <iostream>

namespace MyNamespace {
    int namespaceVar = 42;
}

int main() {
    std::cout << "Namespace variable: " << MyNamespace::namespaceVar << std::endl;
}
```

## Class scope

Identifiers declared within a class have a class scope.
They can be accessed using the class name and the scope resolution operator `::` or, for non-static members, an object of the class and the dot `.` or arrow `->` operator.

```cpp
#include <iostream>

class MyClass {
public:
    static int staticMember;
    int nonStaticMember;

    MyClass(int value) : nonStaticMember(value) {}
};

int MyClass::staticMember = 7;

int main() {
    MyClass obj(10);
    std::cout << "Static member: " << MyClass::staticMember << std::endl;
    std::cout << "Non-static member: " << obj.nonStaticMember << std::endl;
}
```

## Namespaces

In C++, a namespace is a named scope or container that is used to organize and enclose a collection of code elements, such as variables, functions, classes, and other namespaces.
They are mainly used to divide and manage the code base, giving developers control over name collisions and the specialization of code.

```cpp
namespace identifier {
    // code elements
}
```

### Using Namespaces

To access elements within a namespace, you can use the scope resolution operator `::`.

#### Declaring and accessing a namespace

```cpp
#include <iostream>

namespace animals {
    std::string dog = "Bobby";
    std::string cat = "Lilly";
}

int main() {
    std::cout << "Dog's name: " << animals::dog << std::endl;
    std::cout << "Cat's name: " << animals::cat << std::endl;

    return 0;
}
```

#### Nesting namespaces

```cpp
#include <iostream>

namespace outer {
    int x = 10;

    namespace inner {
        int y = 20;
    }
}

int main() {
    std::cout << "Outer x: " << outer::x << std::endl;
    std::cout << "Inner y: " << outer::inner::y << std::endl;

    return 0;
}
```

### `using` Keyword

You can use the `using` keyword to import namespaced elements into the current scope.
However, this might lead to name conflicts if multiple namespaces have elements with the same name.

#### Using a single element from a namespace

```cpp
#include <iostream>

namespace animals {
    std::string dog = "Bobby";
    std::string cat = "Lilly";
}

int main() {
    using animals::dog;
    
    std::cout << "Dog's name: " << dog << std::endl;

    return 0;
}
```

#### Using the entire namespace

```cpp
#include <iostream>

namespace animals {
    std::string dog = "Bobby";
    std::string cat = "Lilly";
}

int main() {
    using namespace animals;
    
    std::cout << "Dog's name: " << dog << std::endl;
    std::cout << "Cat's name: " << cat << std::endl;

    return 0;
}
```
