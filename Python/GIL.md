# Global Interpreter Lock (GIL)

The Python Global Interpreter Lock or GIL, in simple words, is a mutex (or a lock) that allows only one thread to hold the control of the Python interpreter.

This means that only one thread can be in a state of execution at any point in time.
The impact of the GIL isn’t visible to developers who execute single-threaded programs, but it can be a performance bottleneck in CPU-bound and multi-threaded code.

## What Problem Did the GIL Solve for Python?

Python uses reference counting for memory management.
It means that objects created in Python have a reference count variable that keeps track of the number of references that point to the object.
When this count reaches zero, the memory occupied by the object is released.

The problem was that this reference count variable needed protection from race conditions where two threads increase or decrease its value simultaneously.
If this happens, it can cause either leaked memory that is never released or, even worse, incorrectly release the memory while a reference to that object still exists.
This can cause crashes or other “weird” bugs in your Python programs.

This reference count variable can be kept safe by adding locks to all data structures that are shared across threads so that they are not modified inconsistently.

But adding a lock to each object or groups of objects means multiple locks will exist which can cause another problem—Deadlocks (deadlocks can only happen if there is more than one lock).
Another side effect would be decreased performance caused by the repeated acquisition and release of locks.

The GIL is a single lock on the interpreter itself which adds a rule that execution of any Python bytecode requires acquiring the interpreter lock.
This prevents deadlocks (as there is only one lock) and doesn’t introduce much performance overhead. But it effectively makes any CPU-bound Python program single-threaded.

The GIL, although used by interpreters for other languages like Ruby, is not the only solution to this problem.
Some languages avoid the requirement of a GIL for thread-safe memory management by using approaches other than reference counting, such as garbage collection.

On the other hand, this means that those languages often have to compensate for the loss of single threaded performance benefits of a GIL by adding other performance boosting features like JIT compilers.

## How to Deal With Python’s GIL

- Multi-processing vs multi-threading: The most popular way is to use a multi-processing approach where you use multiple processes instead of threads.
- Alternative Python interpreters: GIL exists only in the original Python implementation that is CPython. If your program, with its libraries, is available for one of the other implementations then you can try them out as well.
- Just wait it out: Some of the brightest minds in the Python community are working to remove the GIL from CPython. One such attempt is known as the Gilectomy.
