# Templates

Templates in C++ are a powerful feature that allows you to write generic code, meaning that you can write a single function or class that can work with different data types.
This means you do not need to write separate functions or classes for each data type you want to work with.

## Template Functions

```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
```

## Template Classes

```cpp
template <typename T1, typename T2>
class Pair {
public:
    T1 first;
    T2 second;

    Pair(T1 first, T2 second) : first(first), second(second) {}
};
```

## Template Specialization

Template specialization is a way to customize or modify the behavior of a template for a specific type or a set of types.
This can be useful when you want to optimize the behavior or provide specific implementation for a certain type, without affecting the overall behavior of the template for other types.

There are two main ways you can specialize a template:

- Full specialization: This occurs when you provide a specific implementation for a specific type or set of types.
- Partial specialization: This occurs when you provide a more general implementation for a subset of types that match a certain pattern or condition.

### Full Template Specialization

Full specialization is used when you want to create a separate implementation of a template for a specific type.
To do this, you need to use keyword `template<>` followed by the function template with the desired specialized type.

```cpp
#include <iostream>

template <typename T>
void printData(const T& data) {
    std::cout << "General template: " << data << std::endl;
}

template <>
void printData(const char* const & data) {
    std::cout << "Specialized template for const char*: " << data << std::endl;
}

int main() {
    int a = 5;
    const char* str = "Hello, world!";
    printData(a); // General template: 5
    printData(str); // Specialized template for const char*: Hello, world!
}
```

### Partial Template Specialization

Partial specialization is used when you want to create a separate implementation of a template for a subset of types that match a certain pattern or condition.

```cpp
#include <iostream>

template <typename K, typename V>
class MyPair {
public:
    MyPair(K k, V v) : key(k), value(v) {}

    void print() const {
        std::cout << "General template: key = " << key << ", value = " << value << std::endl;
    }

private:
    K key;
    V value;
};

template <typename T>
class MyPair<T, int> {
public:
    MyPair(T k, int v) : key(k), value(v) {}

    void print() const {
        std::cout << "Partial specialization for int values: key = " << key
                  << ", value = " << value << std::endl;
    }

private:
    T key;
    int value;
};

int main() {
    MyPair<double, std::string> p1(3.2, "example");
    MyPair<char, int> p2('A', 65);
    p1.print(); // General template: key = 3.2, value = example
    p2.print(); // Partial specialization for int values: key = A, value = 65
}
```

## Variadic Templates

Variadic templates are a feature in C++11 that allows you to define a template with a variable number of arguments.
This is especially useful when you need to write a function or class that can accept different numbers and types of arguments.

```cpp
#include <iostream>

// Base case for recursion
template <typename T>
T sum(T t) {
  return t;
}

// Variadic template
template <typename T, typename... Args>
T sum(T t, Args... args) {
  return t + sum(args...);
}

int main() {
  int result = sum(1, 2, 3, 4, 5);  // expands to 1 + 2 + 3 + 4 + 5
  std::cout << "The sum is: " << result << std::endl;

  return 0;
}
```
