# Rust

## Ownership

Ownership in Rust to make memory safety guarantees without needing a garbage collector.

It is a set of rules that govern control a Rust program manages memory.

Here are the rules:

- Each value in Rust has an owner.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

## Reference

Due to the rule that only one owner for the object at a time, Rust introduces the concept of Reference.

Reference is a pointer to the pointer which points to the actual data.
