# Pointers

A pointer is a variable that stores the memory address of another variable (or function). It points to the location of the variable in memory, and it allows you to access or modify the value indirectly.

```cpp
dataType *pointerName;
```

```cpp
int num = 10;
int *ptr = &num;  // Pointer 'ptr' now points to the memory address of 'num'
int value = *ptr; // Value now contains the value of the variable that 'ptr' points to (i.e., 10)
```

## Function Pointer

```cpp
int add(int a, int b)
{
  return a + b;
}

int main()
{
  int (*funcptr) (int, int) = add; // Pointer 'funcptr' now points to the functions 'add'
  funcptr(4, 5); // Return 9
}
```

## References

A reference can be considered as a constant pointer (not to be confused with a pointer to a constant value) which always points to (references) the same object.

### Declaration and Initialization

To declare a reference, use the `&` symbol followed by the variable type and the reference's name. Note that you must initialize a reference when you declare it.

```cpp
int var = 10;        // Declare an integer variable
int& ref = var;      // Declare a reference that "points to" var
```

### Usage

You can use the reference just like you'd use the original variable.
When you change the value of the reference, the value of the original variable also changes, because they both share the same memory location.

```cpp
var = 20;            // Sets the value of var to 20
std::cout << ref << std::endl; // Outputs 20

ref = 30;            // Sets the value of ref to 30
std::cout << var << std::endl; // Outputs 30
```

### Function Parameters

You can use references as function parameters to create an alias for an argument.
This is commonly done when you need to modify the original variable or when passing an object of considerable size to avoid the cost of copying.

```cpp
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
   int x = 5, y = 10;
   std::cout << "Before Swap: x = " << x << " y = " << y << std::endl; // Outputs 5 10
   
   swap(x, y);
   std::cout << "After Swap: x = " << x << " y = " << y << std::endl;  // Outputs 10 5
}
```

## Smart Pointers

### unique_ptr

`std::unique_ptr` is a smart pointer provided by the C++ Standard Library. It is a template class that is used for managing single objects or arrays.

`unique_ptr` works on the concept of exclusive ownership - meaning only one `unique_ptr` is allowed to own an object at a time. This ownership can be transferred or moved, but it cannot be shared or copied.

This concept helps to prevent issues like dangling pointers, reduce memory leaks, and eliminates the need for manual memory management. When the unique_ptr goes out of scope, it automatically deletes the object it owns.

#### Creating a unique_ptr

```cpp
#include <iostream>
#include <memory>

int main() {
    std::unique_ptr<int> p1(new int(5)); // Initialize with pointer to a new integer
    std::unique_ptr<int> p2 = std::make_unique<int>(10); // Preferred method (C++14 onwards)

    std::cout << *p1 << ", " << *p2 << std::endl;
    return 0;
}
```

#### Transferring Ownership

```cpp
#include <iostream>
#include <memory>

int main() {
    std::unique_ptr<int> p1(new int(5));

    std::unique_ptr<int> p2 = std::move(p1); // Ownership is transferred from p1 to p2

    if (p1) {
        std::cout << "p1 owns the object" << std::endl;
    } else if (p2) {
        std::cout << "p2 owns the object" << std::endl;
    }

    return 0;
} 
```

#### Using unique_ptr with Custom Deleters

```cpp
#include <iostream>
#include <memory>

struct MyDeleter {
    void operator()(int* ptr) {
        std::cout << "Custom Deleter: Deleting pointer" << std::endl;
        delete ptr;
    }
};

int main() {
    std::unique_ptr<int, MyDeleter> p1(new int(5), MyDeleter());
    return 0; // Custom Deleter will be called when p1 goes out of scope
}
```

### shared_ptr

A `shared_ptr` is a type of smart pointer in C++ that allows multiple pointers to share ownership of a dynamically allocated object.
The object will be automatically deallocated only when the last `shared_ptr` that points to it is destroyed.

When using a `shared_ptr`, the reference counter is automatically incremented every time a new pointer is created, and decremented when each pointer goes out of scope.
Once the reference counter reaches zero, the system will clean up the memory.

```cpp
#include <iostream>
#include <memory>

class MyClass {
public:
    MyClass() { std::cout << "Constructor is called." << std::endl; }
    ~MyClass() { std::cout << "Destructor is called." << std::endl; }
};

int main() {
    // create a shared pointer to manage the MyClass object
    std::shared_ptr<MyClass> ptr1(new MyClass());
    
    {
        // create another shared pointer and initialize it with the previously created pointer
        std::shared_ptr<MyClass> ptr2 = ptr1;

        std::cout << "Inside the inner scope." << std::endl;
        // both pointers share the same object, and the reference counter has been increased to 2
    }

    std::cout << "Outside the inner scope." << std::endl;
    // leaving the inner scope will destroy ptr2, and the reference counter is decremented to 1
    
    // the main function returns, ptr1 goes out of scope, and the reference counter becomes 0
    // this causes the MyClass object to be deleted and the destructor is called
}
```

### weak_ptr

A `weak_ptr` is a type of smart pointer in C++ that adds a level of indirection and safety to a raw pointer.
It is mainly used to break reference cycles in cases where two objects have shared pointers to each other, or when you need a non-owning reference to an object that is managed by a `shared_ptr`.

A `weak_ptr` does not increase the ownership reference count of the object it points to, which is a key difference between `weak_ptr` and `shared_ptr`.
The control block associated with the object maintains two counts: one for the number of `shared_ptr`s (ownership count) and another for the number of `weak_ptr`s (weak count).
The existence of `weak_ptr`s does not prevent the object from being deleted; the object is destroyed once the last `shared_ptr` that owns it is destroyed or reset, even if `weak_ptr`s are still referencing the object.
However, the control block itself is not deallocated until both the ownership count reaches zero and the weak count also reaches zero, allowing `weak_ptr`s to safely detect whether the object has already been deleted.

To use a `weak_ptr`, you must convert it to a `shared_ptr` using the `lock()` function, which tries to create a new `shared_ptr` that shares ownership of the object.
If successful, the object's reference count is increased and you can use the returned `shared_ptr` to safely access the object.

```cpp
#include <iostream>
#include <memory>

class MyClass {
public:
    void DoSomething() {
        std::cout << "Doing something...\n";
    }
};

int main() {
    std::weak_ptr<MyClass> weak;

    {
        std::shared_ptr<MyClass> shared = std::make_shared<MyClass>();
        weak = shared;

        if(auto sharedFromWeak = weak.lock()) {
            sharedFromWeak->DoSomething(); // Safely use the object
            std::cout << "Shared uses count: " << sharedFromWeak.use_count() << '\n'; // 2
        }
    }

    // shared goes out of scope and the MyClass object is destroyed

    if(auto sharedFromWeak = weak.lock()) {
        // This block will not be executed because the object is destroyed
    }
    else {
        std::cout << "Object has been destroyed\n";
    }

    return 0;
}
```

#### Uses cases for weak_ptr

##### Breaking Circular Dependencies

One of the primary uses of weak pointers is to break circular dependencies between shared pointers.
This prevents memory leaks that can occur when objects reference each other in a cycle.

```cpp
class A {
  std::weak_ptr<B> bptr;
};

class B {
  std::weak_ptr<A> aptr;  
};
```

##### Observers Without Ownership

Weak pointers allow an object to observe another object without taking ownership of it.
This is useful when you want to check if an object still exists without extending its lifetime.

```cpp
class Observer {
  std::weak_ptr<Subject> subject;
  
  void update() {
    std::shared_ptr<Subject> locked = subject.lock();
    if (locked) {
      // Subject still exists, update logic here
    }
  }
};
```

##### Temporary Access in Asynchronous Operations

Weak pointers are useful when you need temporary access to an object in asynchronous operations.
They allow checking if the object still exists before accessing it.

```cpp
void asyncOperation(std::weak_ptr<MyClass> weakSelf) {
  if (std::shared_ptr<MyClass> self = weakSelf.lock()) {
    // Object still exists, use self
  }
}
```

##### Thread Safety

Weak pointers provide thread-safe access to shared objects without risking deadlocks.
They allow checking for existence atomically.

##### Checking Object Validity

Weak pointers can be used to check if an object is still valid after some time has passed.
This is useful for caching mechanisms.

```cpp
if (auto obj = weakPtr.lock()) {
  // Object still exists, use obj
} else {
  // Object no longer exists
}
```

## Raw Pointers

Raw pointers in C++ are low-level constructs that directly hold a memory address.
They can be used for manually allocating memory, creating dynamic arrays, and passing values efficiently, among other things.

### `new` Operator

The `new` operator is used to allocate memory on the heap.
The memory allocated using `new` remains available until you explicitly deallocate it using the corresponding delete operator.

```cpp
int* ptr = new int; // Dynamically allocates an int on the heap
*ptr = 42; // Assigns the value 42 to the allocated int
```

### `delete` Operator

The `delete` operator is used to deallocate memory that has been allocated using `new`.
After memory is deallocated, its available to be reallocated for other purposes.'
Failing to properly deallocate memory can lead to memory leaks.

```cpp
int* ptr = new int; // Dynamically allocates an int on the heap
*ptr = 42; // Assigns the value 42 to the allocated int

delete ptr; // Deallocates the memory assigned to ptr
```

### `new[]` and `delete[]` Operators

The `new[]` and `delete[]` operators are used for allocating and deallocating memory for an array of objects.
The syntax for `new[]` and `delete[]` is very similar to that of `new` and `delete`.

```cpp
int n = 10;
int* arr = new int[n]; // Dynamically allocates an array of 10 integers on the heap

// Set some values in the array
for (int i = 0; i < n; i++) {
  arr[i] = i;
}

delete[] arr; // Deallocates the memory assigned to the array
```
  