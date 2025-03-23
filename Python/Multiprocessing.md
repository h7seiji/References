# Multiprocessing

```python
from multiprocessing import Lock, Process, Queue, current_process
import time
import queue # imported for using queue.Empty exception


def do_job(tasks_to_accomplish, tasks_that_are_done):
    while True:
        try:
            '''
                try to get task from the queue. get_nowait() function will 
                raise queue.Empty exception if the queue is empty. 
                queue(False) function would do the same task also.
            '''
            task = tasks_to_accomplish.get_nowait()
        except queue.Empty:

            break
        else:
            '''
                if no exception has been raised, add the task completion 
                message to task_that_are_done queue
            '''
            print(task)
            tasks_that_are_done.put(task + ' is done by ' + current_process().name)
            time.sleep(.5)
    return True


def main():
    number_of_task = 10
    number_of_processes = 4
    tasks_to_accomplish = Queue()
    tasks_that_are_done = Queue()
    processes = []

    for i in range(number_of_task):
        tasks_to_accomplish.put("Task no " + str(i))

    # creating processes
    for w in range(number_of_processes):
        p = Process(target=do_job, args=(tasks_to_accomplish, tasks_that_are_done))
        processes.append(p)
        p.start()

    # completing process
    for p in processes:
        p.join()

    # print the output
    while not tasks_that_are_done.empty():
        print(tasks_that_are_done.get())

    return True


if __name__ == '__main__':
    main()
```

## Process class

Python multiprocessing `Process` class is an abstraction that sets up another Python process, provides it to run code and a way for the parent application to control execution.
There are two important functions that belongs to the `Process` class - `start()` and `join()` function.
At first, we need to write a function, that will be run by the process.
Then, we need to instantiate a process object.
If we create a process object, nothing will happen until we tell it to start processing via `start()` function.
Then, the process will run and return its result.
After that we tell the process to complete via `join()` function.
Without `join()` function call, process will remain idle and won’t terminate.
So if you create many processes and don’t terminate them, you may face scarcity of resources.
Then you may need to kill them manually.
One important thing is, if you want to pass any argument through the process you need to use `args` keyword argument.

```python
from multiprocessing import Process


def print_func(continent='Asia'):
    print('The name of continent is : ', continent)

if __name__ == "__main__":  # confirms that the code is under main function
    names = ['America', 'Europe', 'Africa']
    procs = []
    proc = Process(target=print_func)  # instantiating without any argument
    procs.append(proc)
    proc.start()

    # instantiating process with arguments
    for name in names:
        # print(name)
        proc = Process(target=print_func, args=(name,))
        procs.append(proc)
        proc.start()

    # complete the processes
    for proc in procs:
        proc.join()
```

## Queue class

Python Multiprocessing modules provides `Queue` class that is exactly a First-In-First-Out data structure.
They can store any pickle Python object (though simple ones are best) and are extremely useful for sharing data between processes.
Queues are specially useful when passed as a parameter to a Process’ target function to enable the Process to consume data.
By using `put()` function we can insert data to then queue and using `get()` we can get items from queues.

```python
from multiprocessing import Queue

colors = ['red', 'green', 'blue', 'black']
cnt = 1
# instantiating a queue object
queue = Queue()
print('pushing items to queue:')
for color in colors:
    print('item no: ', cnt, ' ', color)
    queue.put(color)
    cnt += 1

print('\npopping items from queue:')
cnt = 0
while not queue.empty():
    print('item no: ', cnt, ' ', queue.get())
    cnt += 1
```

## Lock class

It allows code to claim lock so that no other process can execute the similar code until the lock has be released.
So the task of `Lock` class is mainly two.
One is to claim lock and other is to release the lock.
To claim lock the, `acquire()` function is used and to release lock `release()` function is used.

## Pool

Python multiprocessing Pool can be used for parallel execution of a function across multiple input values, distributing the input data across processes (data parallelism).

```python
from multiprocessing import Pool

import time

work = (["A", 5], ["B", 2], ["C", 1], ["D", 3])


def work_log(work_data):
    print(" Process %s waiting %s seconds" % (work_data[0], work_data[1]))
    time.sleep(int(work_data[1]))
    print(" Process %s Finished." % work_data[0])


def pool_handler():
    p = Pool(2)
    p.map(work_log, work)


if __name__ == '__main__':
    pool_handler()
```
