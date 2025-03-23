# Threading

```python
import logging
import threading
import time

def thread_function(name):
    logging.info("Thread %s: starting", name)
    time.sleep(2)
    logging.info("Thread %s: finishing", name)

if __name__ == "__main__":
    format = "%(asctime)s: %(message)s"
    logging.basicConfig(format=format, level=logging.INFO,
                        datefmt="%H:%M:%S")

    logging.info("Main    : before creating thread")
    x = threading.Thread(target=thread_function, args=(1,))
    logging.info("Main    : before running thread")
    x.start()
    logging.info("Main    : wait for the thread to finish")
    x.join()    # Wait for the thread x to complete running
    logging.info("Main    : all done")
```

## Daemon Threads

In computer science, a daemon is a process that runs in the background.

Python threading has a more specific meaning for daemon.
A daemon thread will shut down immediately when the program exits.
One way to think about these definitions is to consider the daemon thread a thread that runs in the background without worrying about shutting it down.

If a program is running Threads that are not daemons, then the program will wait for those threads to complete before it terminates.
Threads that are daemons, however, are just killed wherever they are when the program is exiting.

## Working With Many Threads

### Threads list

```python
import logging
import threading
import time

def thread_function(name):
    logging.info("Thread %s: starting", name)
    time.sleep(2)
    logging.info("Thread %s: finishing", name)

if __name__ == "__main__":
    format = "%(asctime)s: %(message)s"
    logging.basicConfig(format=format, level=logging.INFO,
                        datefmt="%H:%M:%S")

    threads = list()
    for index in range(3):
        logging.info("Main    : create and start thread %d.", index)
        x = threading.Thread(target=thread_function, args=(index,))
        threads.append(x)
        x.start()

    for index, thread in enumerate(threads):
        logging.info("Main    : before joining thread %d.", index)
        thread.join()
        logging.info("Main    : thread %d done", index)
```

### ThreadPoolExecutor

```python
import logging
import threading
import time
import concurrent.futures

def thread_function(name):
    logging.info("Thread %s: starting", name)
    time.sleep(2)
    logging.info("Thread %s: finishing", name)

if __name__ == "__main__":
    format = "%(asctime)s: %(message)s"
    logging.basicConfig(format=format, level=logging.INFO,
                        datefmt="%H:%M:%S")

    with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:
        executor.map(thread_function, range(3))
```

## Basic Synchronization Using Lock

```python
class FakeDatabase:
    def __init__(self):
        self.value = 0
        self._lock = threading.Lock()

    def locked_update(self, name):
        logging.info("Thread %s: starting update", name)
        logging.debug("Thread %s about to lock", name)
        with self._lock:
            logging.debug("Thread %s has lock", name)
            local_copy = self.value
            local_copy += 1
            time.sleep(0.1)
            self.value = local_copy
            logging.debug("Thread %s about to release lock", name)
        logging.debug("Thread %s after release", name)
        logging.info("Thread %s: finishing update", name)
```

## Threading Objects

### Semaphore

A Semaphore is a counter with a few special properties.
The first one is that the counting is atomic.
This means that there is a guarantee that the operating system will not swap out the thread in the middle of incrementing or decrementing the counter.

The internal counter is incremented when you call `.release()` and decremented when you call `.acquire()`.

The next special property is that if a thread calls `.acquire()` when the counter is zero, that thread will block until a different thread calls `.release()` and increments the counter to one.

Semaphores are frequently used to protect a resource that has a limited capacity.
An example would be if you have a pool of connections and want to limit the size of that pool to a specific number.

### Timer

A threading.Timer is a way to schedule a function to be called after a certain amount of time has passed. You create a Timer by passing in a number of seconds to wait and a function to call:

```python
t = threading.Timer(30.0, my_function)
```

You start the Timer by calling `.start()`.
The function will be called on a new thread at some point after the specified time, but be aware that there is no promise that it will be called exactly at the time you want.

If you want to stop a Timer that you’ve already started, you can cancel it by calling `.cancel()`.
Calling `.cancel()` after the Timer has triggered does nothing and does not produce an exception.

A Timer can be used to prompt a user for action after a specific amount of time.
If the user does the action before the Timer expires, `.cancel()` can be called.

### Barrier

A threading.Barrier can be used to keep a fixed number of threads in sync.
When creating a Barrier, the caller must specify how many threads will be synchronizing on it.
Each thread calls `.wait()` on the Barrier.
They all will remain blocked until the specified number of threads are waiting, and then the are all released at the same time.

Remember that threads are scheduled by the operating system so, even though all of the threads are released simultaneously, they will be scheduled to run one at a time.

One use for a Barrier is to allow a pool of threads to initialize themselves.
Having the threads wait on a Barrier after they are initialized will ensure that none of the threads start running before all of the threads are finished with their initialization.
