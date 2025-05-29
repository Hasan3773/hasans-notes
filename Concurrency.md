The ability for different parts or a program to be ran out-of-order or in partial order while still having the same final result. 

Concurrency vs Parallelism:
- in concurrency the different threads all have a shared memory location. Whereas in parallelism, the different process's don't necessarily share memory but are just run in parallel.

Thread vs Process
- Threads are a very lightweight version of process's that are quicker to start up and shut down.

Thread
- The smallest unit of execution in a process that executes instructions serially.
- When a process has multiple threads is called multithreading.
- Each thread usually has a section private to itself and a section it shares with other threads. 

Critical Section
- Any piece of code (which exposes shared data / resources) that has the possibility of being executed concurrently by more than one thread.
  
Mutex (mutual exclusion)
- Used to guard shared data, a thread can take a mutex, it then is the only one who has access to that resource. Once the thread releases the mutex other threads can then grab the mutex.
  
Semaphore
- Used to limit access to a collection of resources, like a limited number of permits to give out. 

Deadlock
- The permanent blockage of a shared resource?
  
Livelock
- Two process that continuously change stats without doing useful work. I.e. to people crisscrossing each other while trying to pass each other in the hallway. 
  
Starvation 
- Other threads are too greedy and a thread never gets access to resources. 

Race Conditions
- Multiple threads changing a shared resource and the final value is uncertain.

A concurrency privative is like an object used in concurrent programming, what other ones are there other than threads? 

Questions:
- Can process's have a shared section?
- How do semaphores stop race conditions?
-