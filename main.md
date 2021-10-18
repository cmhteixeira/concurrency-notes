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

