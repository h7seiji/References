# Struct

The main difference between a structure and a class is their default access specifier: members of a structure are public by default, while members of a class are private.

```cpp
struct Employee {
    int id;
    std::string name;
    float salary;
};

Employee e1; // create an object of the 'Employee' structure

e1.id = 1;
e1.name = "John Doe";
e1.salary = 40000;
```
