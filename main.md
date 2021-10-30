## Stuff

1. The JVM can reorder program statements.  
1.1. On a per thread basis, if it can prove the reordering does not affect serial execution, the JVM is allowed to change order of the statements as the programmer writes them on the source code. Remember, this only occurs if the JVM is certain the meaning from the point of view of a single thread is not affected. Obviously this has consequences if that thread operates over shared mutable data.

2. The JVM does not necessarily push changes to shared variables made within a thread immeditily.  
2.1. For performance reason, it can "record" the change on local caches and "commit" later.  
2.2. To avoid this, you must syncrhonzie the variable: use `syncrhonize` [or `@volatile` I think]


## Implementations
### Java

#### java.util.concurrent.BlockingQueue

## Stuff
Concurrent queues => usefull to implement the producer-consumer pattern.  
Concurrent maps and sets => usefull to encode program state.  
This is a fundamental difference.

## Concurrect data structures
### Treiber stack
```scala
class TreiberStack[A] {
  def push(a: A): Unit = ???
  def pop(): A = ???
}
```

- Concurrent stack abstraction
- It is a shared stack
- Remember stacks are LIFO

## Synchronizing mutable state

### Asymmetric solution
Asymmetric solutions are characterized by the reader and writer threads executing different code before entering the critical section

## Problems
### Readers/Writers problem

- Any number of threads. Some are readers, some are writers.  
- Any number of reader threads can access the critical section at the same time.
- Only a single writer thread might be accessing the critical section at a given time.
- No writer thread can have access if there is a single reader thread with access.

Possible scenarios:
1. N reader threads and 0 writer threads, where N>0
2. 0 reader threads and 1 writer thread.
3. 0 reader threads and 0 writer threads.

### Producer/Consumer problem


## Mutex ≠ Semaphore(1) ⚠️
**It is a critical to understand this!!**  
- On a Mutex, only the thread holding the lock can release it.
- On a Semaphore, any thread can release (i.e. increment) it.

This is misunderstood by most programmers. Even some prominent text books
equate the two. Regardless it is factually wrong.  
Citation from `Operating Systems Internals and Design Principles, 9th Edition, Global Edition` by `William Stallings` on page `247` of section `5.4`:
> A concept related to the binary semaphore is the mutual exclusion lock (mutex).
A mutex is a programming flag used to grab and release an object. When data are
acquired that cannot be shared, or processing is started that cannot be performed
simultaneously elsewhere in the system, the mutex is set to lock (typically zero),
which blocks other attempts to use it. The mutex is set to unlock when the data are
no longer needed or the routine is finished. A key difference between the a mutex
and a binary semaphore is that the process that locks the mutex (sets the value to
zero) must be the one to unlock it (sets the value to 1). In contrast, it is possible for
one process to lock a binary semaphore and for another to unlock it.

Relevant SO thread [here](https://stackoverflow.com/questions/34519/what-is-a-semaphore/40238#40238).

## Starvation vs. DeadLock
These are different concepts.  
An algorithm might be deadlock free but still expose himself to starvation.  


