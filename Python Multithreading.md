When multithreading, each thread has its own stack memory but the heap is shared. The function results from the call stack of each thread are stored on the heap so that the other threads can operate asynchronously.

Multithreading - The use of multiple threads in a single process. 

Thread -  A basic unit of execution in a process. 

Process - Series of actions done to execute a program.

Benefits: Increased responsiveness, Resource sharing, Utilization of multiprocessor architecture (a single thread process can only use a single CPU but a multi-thread process can utilize multiple processors)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeH-LvrohxI02FtxLDbMRq49yBE_qnpepl2aDHBMj-awz5FBTZ2GSznTSSKly4VpKM3uXnawYUmOFFtRTgCXLc2f4BtNSq1Vns59jTgTdpQaVxWZN6eyDwqO2AbkFHBTPfwAQX6kmgr7VJx29M6F5FPwDQ?key=96Zz1iNouwiYhGNilCw3Ng)

Difference between Multi-threading & Multi-processing: By formal definition, multithreading refers to the ability of a processor to execute multiple threads concurrently, where each thread runs a process. Whereas multiprocessing refers to the ability of a system to run multiple processors in parallel, where each processor can run one or more threads.

Functions:
- .is_alive() - returns whether the thread is still running
- .join() - delays execution of a program until target thread has been "read"?
- .local() - returns local thread object with data specific to that thread?
- .run() - executes target function belonging to a given thread
- .start() - activates and prompts? a thread object to be run
- .Thread() - returns a thread object that can run a function 

Threading Solutions in Python:
- Barrier - 
- Lock
- Event
- Semaphore
- Condition
``` Python 
t1 = threading.Thread(target=class.method, args=(5,))
t1.start()
t1.join()
```

Semaphore:
```python
from threading import Semaphore

class Foo:
    def __init__(self):
        self.sema = (Semaphore(-1)
        
    def first(self, printFirst):
        printFirst()
        self.sema.release()
        
    def second(self, printSecond):
        self.sema.acquire()
        printSecond()
        self.sema.release()
            
    def third(self, printThird):
        self.sema.acquire()
        printThird()
```

Mutex:
```python
from threading import Lock

class Foo:
    def __init__(self):
        self.locks = (Lock(),Lock())
        self.locks[0].acquire()
        self.locks[1].acquire()
        
    def first(self, printFirst):
        printFirst()
        self.locks[0].release()
        
    def second(self, printSecond):
        with self.locks[0]:
            printSecond()
            self.locks[1].release()
            
            
    def third(self, printThird):
        with self.locks[1]:
            printThird()
```

Barrier:
```python
from threading import Barrier

class Foo:
    def __init__(self):
        self.first_barrier = Barrier(2)
        self.second_barrier = Barrier(2)
            
    def first(self, printFirst):
        printFirst()
        self.first_barrier.wait()
        
    def second(self, printSecond):
        self.first_barrier.wait()
        printSecond()
        self.second_barrier.wait()
            
    def third(self, printThird):
        self.second_barrier.wait()
        printThird()
```