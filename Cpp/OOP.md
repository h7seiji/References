# Object-Oriented Programming (OOP) in C++

Object-oriented programming (OOP) is a programming paradigm that uses objects, which are instances of classes, to perform operations and interact with each other.

## Encapsulation

Encapsulation is the concept of bundling data and functions that operate on that data within a single unit, such as a class.
It helps to hide the internal implementation details of a class and expose only the necessary information and functionalities.
In C++, you can use access specifiers like `public`, `private`, and `protected` to control the visibility and accessibility of class members.

```cpp
class Dog {
private:
    std::string name;
    int age;

public:
    void setName(std::string n) {
        name = n;
    }

    void setAge(int a) {
        age = a;
    }

    void bark() {
        std::cout << name << " barks!" << std::endl;
    }
};
```

## Inheritance

Inheritance is the concept of deriving new classes from existing ones, which enables code reusability and organization.
In C++, inheritance is achieved by using a colon `:` followed by the base class’ access specifier and the base class name.

```cpp
class Animal {
public:
    void breathe() {
        std::cout << "I can breathe" << std::endl;
    }
};

class Dog : public Animal {
public:
    void bark() {
        std::cout << "Dog barks!" << std::endl;
    }
};

Dog myDog;
myDog.breathe(); // Output: I can breathe
myDog.bark(); // Output: Dog barks!
```

## Polymorphism

Polymorphism allows you to use a single interface to represent different types.
In C++, it’s mainly achieved using function overloading, virtual functions, and overriding.

```cpp
class Animal {
public:
    virtual void makeSound() {
        std::cout << "The Animal makes a sound" << std::endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override {
        std::cout << "Dog barks!" << std::endl;
    }
};

class Cat : public Animal {
public:
    void makeSound() override {
        std::cout << "Cat meows!" << std::endl;
    }
};

Animal *animals[2] = {new Dog, new Cat};
animals[0]->makeSound(); // Output: Dog barks!
animals[1]->makeSound(); // Output: Cat meows!
```

### Static Polymorphism

Static polymorphism, also known as compile-time polymorphism, is a type of polymorphism that resolves the types and method calls at compile time rather than at runtime.
This is commonly achieved through the use of function overloading and templates in C++.

#### Function Overloading

Function overloading is a way to create multiple functions with the same name but different parameter lists.
The compiler determines the correct function to call based on the types and number of arguments used when the function is called.

```cpp
#include <iostream>

void print(int i) {
    std::cout << "Printing int: " << i << std::endl;
}

void print(double d) {
    std::cout << "Printing double: " << d << std::endl;
}

void print(const char* s) {
    std::cout << "Printing string: " << s << std::endl;
}

int main() {
    print(5);          // Calls print(int i)
    print(3.14);       // Calls print(double d)
    print("Hello");    // Calls print(const char* s)

    return 0;
}
```

#### Templates

Templates are a powerful feature in C++ that allows you to create generic functions or classes.
The actual code for specific types is generated at compile time, which avoids the overhead of runtime polymorphism.
The use of templates is the main technique to achieve static polymorphism in C++.

```cpp
#include <iostream>

// Template function to print any type
template<typename T>
void print(const T& value) {
    std::cout << "Printing value: " << value << std::endl;
}

int main() {
    print(42);           // int
    print(3.14159);      // double
    print("Hello");      // const char*

    return 0;
}
```

### Dynamic Polymorphism

Dynamic polymorphism is a programming concept in object-oriented languages like C++ where a derived class can override or redefine methods of its base class.
This means that a single method call can have different implementations based on the type of object it is called on.

Dynamic polymorphism is achieved through virtual functions, which are member functions of a base class marked with the `virtual` keyword.
When you specify a virtual function in a base class, it can be overridden in any derived class to provide a different implementation.

```cpp
#include <iostream>

// Base class
class Shape {
public:
    virtual void draw() {
        std::cout << "Drawing a shape" << std::endl; 
    }
};

// Derived class 1
class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a circle" << std::endl; 
    }
};

// Derived class 2
class Rectangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a rectangle" << std::endl;
    }
};

int main() {
    Shape* shape;
    Circle circle;
    Rectangle rectangle;

    // Storing the address of circle
    shape = &circle;

    // Call circle draw function
    shape->draw();  // Drawing a circle

    // Storing the address of rectangle
    shape = &rectangle;

    // Call rectangle draw function
    shape->draw();  // Drawing a rectangle

    return 0;
}
```

#### Virtual Tables

Virtual Tables (or Vtable) are a mechanism used by C++ compilers to support dynamic polymorphism.
In dynamic polymorphism, the appropriate function is called at runtime, depending on the actual object type.

When a class contains a virtual function, the compiler creates a virtual table for that class.
This table contains function pointers to the virtual functions defined in the class.
Each object of that class has a pointer to its virtual table (vptr, virtual pointer), which is automatically initialized by the compiler during object construction.
