# Idioms

C++ idioms are well-established patterns or techniques that are commonly used in C++ programming to achieve a specific outcome.
They help make code efficient, maintainable, and less error-prone.

## Resource Acquisition is Initialization (RAII)

This idiom ensures that resources are always properly acquired and released by tying their lifetime to the lifetime of an object.
When the object gets created, it acquires the resources and when it gets destroyed, it releases them.

```cpp
class Resource {
public:
    Resource() { /* Acquire resource */ }
    ~Resource() { /* Release resource */ }
};

void function() {
    Resource r; // Resource is acquired
    // ...
} // Resource is released when r goes out of scope
```

## Rule of Three

If a class defines any one of the following, it should define all three: copy constructor, copy assignment operator, and destructor.

```cpp
class MyClass {
public:
    MyClass();
    MyClass(const MyClass& other); // Copy constructor
    MyClass& operator=(const MyClass& other); // Copy assignment operator
    ~MyClass(); // Destructor
};
```

## Rule of Five

With C++11, the rule of three was extended to five, covering move constructor and move assignment operator.

```cpp
class MyClass {
public:
    MyClass();
    MyClass(const MyClass& other); // Copy constructor
    MyClass(MyClass&& other); // Move constructor
    MyClass& operator=(const MyClass& other); // Copy assignment operator
    MyClass& operator=(MyClass&& other); // Move assignment operator
    ~MyClass(); // Destructor
};
```

## PImpl (Pointer to Implementation) Idiom

This idiom is used to separate the implementation details of a class from its interface, resulting in faster compile times and the ability to change implementation without affecting clients.

```cpp
// header file
class MyClass {
public:
    MyClass();
    ~MyClass();
    void someMethod();

private:
    class Impl;
    Impl* pImpl;
};

// implementation file
class MyClass::Impl {
public:
    void someMethod() { /* Implementation */ }
};

MyClass::MyClass() : pImpl(new Impl()) {}
MyClass::~MyClass() { delete pImpl; }
void MyClass::someMethod() { pImpl->someMethod(); }
```

## Non-Virtual Interface (NVI)

This enforces a fixed public interface and allows subclasses to only override specific private or protected virtual methods.

```cpp
class Base {
public:
    void publicMethod() {
        // Common behavior
        privateMethod(); // Calls overridden implementation
    }

protected:
    virtual void privateMethod() = 0; // Pure virtual method
};

class Derived : public Base {
protected:
    virtual void privateMethod() override {
        // Derived implementation
    }
};
```

## Curiously Recurring Template Pattern (CRTP)

The Curiously Recurring Template Pattern (CRTP) is a C++ idiom that involves a class template being derived from its own specialization.
This pattern allows for the creation of static polymorphism, which differs from regular runtime polymorphism that relies on virtual functions and inheritance.

CRTP is usually employed when you want to customize certain behavior in the base class without adding the overhead of a virtual function call.
In short, CRTP can be used for achieving compile-time polymorphism without the runtime performance cost.

```cpp
template <typename Derived>
class Base {
public:
    void interface() {
        static_cast<Derived*>(this)->implementation();
    }

    void implementation() {
        std::cout << "Default implementation in Base" << std::endl;
    }
};

class Derived1 : public Base<Derived1> {
public:
    void implementation() {
        std::cout << "Custom implementation in Derived1" << std::endl;
    }
};

class Derived2 : public Base<Derived2> {
    // No custom implementation, so Base::implementation will be used.
};

int main() {
    Derived1 d1;
    d1.interface();  // Output: "Custom implementation in Derived1"

    Derived2 d2;
    d2.interface();  // Output: "Default implementation in Base"

    return 0;
}
```

## Non-Copyable

The non-copyable idiom is a C++ design pattern that prevents objects from being copied or assigned.
It's usually applied to classes that manage resources, like file handles or network sockets, where copying the object could cause issues like resource leaks or double deletions.

To make a class non-copyable, you need to delete the copy constructor and the copy assignment operator.
This can be done explicitly in the class declaration, making it clear to other programmers that copying is not allowed.

```cpp
class NonCopyable {
public:
  NonCopyable() = default;
  ~NonCopyable() = default;

  // Delete the copy constructor
  NonCopyable(const NonCopyable&) = delete;

  // Delete the copy assignment operator
  NonCopyable& operator=(const NonCopyable&) = delete;
};
```

## Erase-remove

The erase-remove idiom is a common C++ technique to efficiently remove elements from a container, particularly from standard sequence containers like `std::vector`, `std::list`, and `std::deque`.
It leverages the standard library algorithms `std::remove` (or `std::remove_if`) and the member function `erase()`.

The idiom consists of two steps:

- `std::remove` (or `std::remove_if`) moves the elements to be removed towards the end of the container and returns an iterator pointing to the first element to remove.
- `container.erase()` removes the elements from the container using the iterator obtained in the previous step.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> numbers = {1, 3, 2, 4, 3, 5, 3};
    
    // Remove all occurrences of 3 from the vector.
    numbers.erase(std::remove(numbers.begin(), numbers.end(), 3), numbers.end());

    for (int number : numbers) {
        std::cout << number << " ";
    }

    return 0;
}
```

## Copy and Swap

Copy-swap is a C++ idiom that leverages the copy constructor and swap function to create an assignment operator.
It follows a simple, yet powerful paradigm: create a temporary copy of the right-hand side object, and swap its contents with the left-hand side object.

Here's a brief summary:

- Copy: Create a local copy of the right-hand side object. This step leverages the copy constructor, providing exception safety and code reuse.
- Swap: Swap the contents of the left-hand side object with the temporary copy. This step typically involves swapping internal pointers or resources, without needing to copy the full contents again.
- Destruction: Destroy the temporary copy. This happens upon the exit of the assignment operator.

```cpp
class String {
    // ... rest of the class ...

    String(const String& other);
    
    friend void swap(String& first, String& second) {
        using std::swap; // for arguments-dependent lookup (ADL)
        swap(first.size_, second.size_);
        swap(first.buffer_, second.buffer_);
    }

    String& operator=(String other) {
        swap(*this, other);
        return *this;
    }
};
```

## Copy-Write

The Copy-Write idiom, sometimes called the Copy-on-Write (CoW) or “lazy copying” idiom, is a technique used in programming to minimize the overhead of copying large objects.
It helps in reducing the number of actual copy operations by using shared references to objects and only copying the data when it's required for modification.

```cpp
#include <iostream>
#include <memory>

class MyString {
public:
    MyString(const std::string &str) : data(std::make_shared<std::string>(str)) {}

    // Use the same shared data for copying.
    MyString(const MyString &other) : data(other.data) { 
        std::cout << "Copied using the Copy-Write idiom." << std::endl;
    }

    // Make a copy only if we want to modify the data.
    void write(const std::string &str) {
        // Check if there's more than one reference.
        if(!data.unique()) {
            data = std::make_shared<std::string>(*data);
            std::cout << "Copy is actually made for writing." << std::endl;
        }
        *data = str;
    }

private:
    std::shared_ptr<std::string> data;
};

int main() {
    MyString str1("Hello");
    MyString str2 = str1; // No copy operation, just shared references.

    str1.write("Hello, World!"); // This is where the actual duplication happens.
    return 0;
}
```
