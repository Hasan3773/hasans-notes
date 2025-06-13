
Parts of a Thread:
- The thread ID
- Program Counter, a value that loads into the hardware… research more
- Registered set, a set of general registers for the thread
- The stack memory for the thread since the heap is shared

Two Types of Threads:
- User Level Threads, info stays at a user level not shared with the OS
- Kernel Level Thread, thread operated by the OS’
 
Implementation:
- Standard library to use is <threads.h>, however currently you have to specify a platform specific library such as POSIX using a header file
- #include <pthread.h>
- pthread_create (thread, attr, start_routine, arg)

Deadlock: When two or more threads try to access the same shared variable at the same time 

Semaphore: A signaling non negative integer variable used in multithreading to prevent critical section 
- Binary Semaphore: if sem value is 1 a thread can access var, if 0 threads cannot, also called mutex lock
- Counting Semaphore: if the sem value is > 0 then a thread can access the critical section but if it = 0  then there are no more resources available so it cannot be accessed
- Normal structure is a wait function (check if sem is valid), critical section, signal function (increment the sem back up)

Mutex: Stands for an object provide MUTual EXclusion between threads, basically a special type of a binary semaphore, it's a locking mechanism that allows threads to access a critical section one at a time, the main issue priority inversion problems where a low priority and high priority task have equal priority, which is solved by the use of a scheduler, difference between this and a binary semaphore is that when a process uses a mutex it takes ownership (I don't fully get this). 

Frameworks: There are two frameworks for multithreading, queues & shared memory. 
  
Race Condition: Basic concept is that one thing goes faster than it should and changes the value of something another thing is using before it should have, giving an undesirable output. The famous consumer - producer problem is an example of a race condition, here is a link to the solution in C: https://www.scaler.com/topics/producer-consumer-problem-in-c


std::mutex
- must be released by the same thread that locks it
- use with a lock: std::lock_guard, std::unique_lock, std::scoped_lock

std::shared_mutex
- allows multiple threads shared access 