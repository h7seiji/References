# Class

```cpp
class Student {
    int roll_no;
    std::string name;
    float marks;

public:
    void set_data(int r, std::string n, float m) {
        roll_no = r;
        name = n;
        marks = m;
    }

    void display() {
        std::cout << "Roll no: " << roll_no
                  << "\nName: " << name
                  << "\nMarks: " << marks << std::endl;
    }
};

Student s1; // create an object of the 'Student' class

s1.set_data(1, "Alice", 95.0);
s1.display();
```

## Multiple Inheritance

Multiple inheritance is a feature in C++ where a class can inherit characteristics (data members and member functions) from more than one parent class.
The concept is similar to single inheritance (where a class inherits from a single base class), but in multiple inheritance, a class can have multiple base classes.

When a class inherits multiple base classes, it becomes a mixture of their properties and behaviors, and can override or extend them as needed.

```cpp
#include <iostream>

// Base class 1
class Animal
{
public:
    void eat()
    {
        std::cout << "I can eat!" << std::endl;
    }
};

// Base class 2
class Mammal
{
public:
    void breath()
    {
        std::cout << "I can breathe!" << std::endl;
    }
};

// Derived class inheriting from both Animal and Mammal
class Dog : public Animal, public Mammal
{
public:
    void bark()
    {
        std::cout << "I can bark! Woof woof!" << std::endl;
    }
};

int main()
{
    Dog myDog;

    // Calling members from both base classes
    myDog.eat();
    myDog.breath();
    
    // Calling a member from the derived class
    myDog.bark();

    return 0;
}
```

### Diamond Inheritance

Diamond inheritance is a specific scenario in multiple inheritance where a class is derived from two or more classes, which in turn, are derived from a common base class.
It creates an ambiguity that arises from duplicating the common base class, which leads to an ambiguous behavior while calling the duplicate members.

To resolve this ambiguity, you can use virtual inheritance.
A virtual base class is a class that is shared by multiple classes using `virtual` keyword in C++.
This ensures that only one copy of the base class is inherited in the final derived class, and thus, resolves the diamond inheritance problem.

```cpp
#include <iostream>

class Base {
public:
    void print() {
        std::cout << "Base class" << std::endl;
    }
};

class Derived1 : virtual public Base {
public:
    void derived1Print() {
        std::cout << "Derived1 class" << std::endl;
    }
};

class Derived2 : virtual public Base {
public:
    void derived2Print() {
        std::cout << "Derived2 class" << std::endl;
    }
};

class Derived3 : public Derived1, public Derived2 {
public:
    void derived3Print() {
        std::cout << "Derived3 class" << std::endl;
    }
};

int main() {
    Derived3 d3;
    d3.print(); // Now, there is no ambiguity in calling the base class function
    d3.derived1Print();
    d3.derived2Print();
    d3.derived3Print();

    return 0;
}
```

## Rule of Zero, Three, and Five

The Rule of Zero, Three, and Five is a set of guidelines for managing object resources in modern C++, related to structures and classes.
These rules deal with the default behavior of constructors, destructors, and other special member functions that are necessary for proper resource management.

### Rule of Zero

The Rule of Zero states that if a class or structure does not explicitly manage resources, it should not define any of the special member functions, i.e., destructor, copy constructor, copy assignment operator, move constructor, and move assignment operator.
The compiler will automatically generate these functions, and the behavior will be correct for managing resources like memory and file handles.

```cpp
struct MyResource {
    std::string name;
    int value;
};
```

### Rule of Three

The Rule of Three states that a class or structure that manages resources should define the following three special member functions:

- Destructor
- Copy constructor
- Copy assignment operator

These functions are necessary for proper resource management, such as releasing memory or correctly handling deep copies.

```cpp
class MyResource {
public:
    // Constructor and destructor
    MyResource() : data(new int[100]) {} 
    ~MyResource() { delete[] data; } 

    // Copy constructor
    MyResource(const MyResource& other) : data(new int[100]) {
        std::copy(other.data, other.data + 100, data);
    }

    // Copy assignment operator
    MyResource& operator=(const MyResource& other) {
        if (&other == this) { return *this; }
        std::copy(other.data, other.data + 100, data);
        return *this;
    }

private:
    int* data;
};
```

### Rule of Five

The Rule of Five extends the Rule of Three to include two additional special member functions:

- Move constructor
- Move assignment operator

Modern C++ introduces move semantics, which allows for more efficient handling of resources by transferring ownership without necessarily copying all the data.

```cpp
class MyResource {
public:
    // Constructors and destructor
    MyResource() : data(new int[100]) {}
    ~MyResource() { delete[] data; }

    // Copy constructor
    MyResource(const MyResource& other) : data(new int[100]) {
        std::copy(other.data, other.data + 100, data);
    }

    // Copy assignment operator
    MyResource& operator=(const MyResource& other) {
        if (&other == this) { return *this; }
        std::copy(other.data, other.data + 100, data);
        return *this;
    }

    // Move constructor
    MyResource(MyResource&& other) noexcept : data(other.data) {
        other.data = nullptr;
    }

    // Move assignment operator
    MyResource& operator=(MyResource&& other) noexcept {
        if (&other == this) { return *this; }
        delete[] data;
        data = other.data;
        other.data = nullptr;
        return *this;
    }

private:
    int* data;
};
```

## Constructors and destructors

### Constructors

Class constructors in C++ are special member functions that are automatically called when an object of a class is created.

- Constructors are invoked automatically when an object of the class is created.
- They are typically used to set initial values for data members of the class.
- Constructors can take parameters, which allows for different ways to create and initialize objects.
- You can define multiple constructors for a class, which is called constructor overloading.

### Destructors

Destructors are special member functions of a class that are automatically called when an object of that class is destroyed.
They are used to clean up resources allocated by the object during its lifetime.

- Named with the tilde symbol `~` followed by the class name.
- Do not take any parameters and do not return any value.
- Cannot be overloaded or static.
- Are called automatically when an object goes out of scope or is explicitly deleted.

```cpp
class MyClass {
private:
    int* data;

public:
    MyClass(int size) {
        data = new int[size];
    }

    ~MyClass() {
        delete[] data;
    }
};
```

## Copy constructor and copy assignment operator

### Copy constructors

Copy constructors are special member functions of a class that are used to create a new object as a copy of an existing object.

- The first parameter is of type `const T&`, where `T` is the class type.
- They are used when an object needs to be initialized with another object of the same class.
- They are typically used to deep copy the contents of the source object to the new object.

### Copy assignment operators

Copy assignment operators are member functions of a class that are used to assign the contents of one object to another object of the same class.
They are called when an object is assigned to another object of the same class.

- The function name is the `operator=` followed by the class name.
- They have no return type.
- They are typically declared as public member functions.
- They are used to perform a deep copy of the source object's contents to the target object.

```cpp
#include <iostream>
#include <string>

class MyClass {
private:
    std::string name;
    int age;

public:
    // Copy constructor
    MyClass(const MyClass& other) : name(other.name), age(other.age) {
        std::cout << "Copy constructor called" << std::endl;
    }

    // Copy assignment operator
    MyClass& operator=(const MyClass& other) {
        name = other.name;
        age = other.age;
        std::cout << "Copy assignment operator called" << std::endl;
        return *this;
    }

    void display() const {
        std::cout << "Name: " << name << ", Age: " << age << std::endl;
    }
};

int main() {
    MyClass obj1("Alice", 30);

    // Copy constructor
    MyClass obj2(obj1);
    obj2.display();

    MyClass obj3;
    obj3 = obj1;  // This calls the copy assignment operator
    obj3.display();

    return 0;
}
```

## Move constructor and move assignment operator

### Move constructors

Move constructors are similar to copy constructors but are designed for more efficient resource transfer. They have the following characteristics:

- The first parameter is of type `T&&`, where `T` is the class type.
- They are used when an object needs to be initialized with an rvalue (temporary) object of the same class.
- They are typically used to transfer ownership of resources from the source object to the new object efficiently.

### Move assignment operators

Move assignment operators are special member functions of a class that are used to assign the contents of one object to another object of the same class, transferring resources efficiently.

- The function name is `operator=` followed by the class name.
- They have no return type.
- They are typically declared as public member functions.
- They are used to transfer resources from the source object to the target object efficiently.

```cpp
#include <iostream>
#include <string>

class MyClass {
private:
    std::string name;
    int age;

public:
    // Move constructor
    MyClass(MyClass&& other) noexcept : name(std::move(other.name)), age(other.age) {
        std::cout << "Move constructor called" << std::endl;
    }

    // Move assignment operator
    MyClass& operator=(MyClass&& other) noexcept {
        name = std::move(other.name);
        age = other.age;
        std::cout << "Move assignment operator called" << std::endl;
        return *this;
    }

    void display() const {
        std::cout << "Name: " << name << ", Age: " << age << std::endl;
    }
};

int main() {
    MyClass obj1("Alice", 30);

    // Move constructor
    MyClass obj3(std::move(obj1));
    obj3.display();

    MyClass obj2;
    obj2 = std::move(obj1);  // This calls the move assignment operator
    obj2.display();

    return 0;
}
```
