# C++ Standard Template Library (STL)

The C++ Standard Template Library (STL) is a collection of header files that provide several data structures, algorithms, and functions to simplify your C++ coding experience.
The primary purpose of the STL is to save time and increase efficiency by providing a ready-to-use set of useful tools.
The most commonly used features of the STL can be divided into three main categories: containers, algorithms, and iterators.

## Containers

Containers are the data structures used for data storage and manipulation in C++.
They are classified into four types: sequence containers, associative containers, unordered associative containers, and container adaptors.

### Sequence Containers

These are linear data structures that store elements in a sequential manner. Examples include:

- std::vector: A dynamic array that grows and shrinks at runtime.
- std::list: A doubly linked list.
- std::deque: A double-ended queue allowing insertion and deletion at both ends.

### Associative Containers

These containers store data in a sorted manner with unique keys. Examples include:

- std::set: A collection of unique elements sorted by keys.
- std::map: A collection of key-value pairs sorted by keys.

### Unordered Associative Containers

These containers store data in an unordered manner using hash tables. Examples include:

- std::unordered_set: A collection of unique elements in no specific order.
- std::unordered_map: A collection of key-value pairs in no specific order.

### Container Adaptors

These are containers based on other existing containers. Examples include:

- std::stack: A LIFO data structure based on deque or list.
- std::queue: A FIFO data structure based on deque or list.
- std::priority_queue: A sorted queue based on vector or deque.

## Algorithms

The STL provides several generic algorithms that can be used to perform various operations on the data stored in containers.
They are divided into five categories: non-modifying sequence algorithms, modifying sequence algorithms, sorting algorithms, sorted range algorithms, and numeric algorithms.

Some examples include std::find, std::replace, std::sort, and std::binary_search.

## Iterators

Iterators are a fundamental concept in the STL, as they provide a unified way to access elements in containers.
Iterators can be thought of as an advanced form of pointers.

Each container has its own iterator type, which can be used to traverse elements and modify values.
The most common iterator operations are begin() and end() for getting iterators pointing to the first and one past the last element of a container, respectively.
