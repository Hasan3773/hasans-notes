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