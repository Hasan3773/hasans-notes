Coding language that is abstracted C with added functionality.

Key Added Functionality:
- OOP
- Memory management
- Freedom of programming structure
- Compiled language so efficient 
- Smart Pointers
- STL library 
- Operator overloading
- Muti threading support 

Compilation Steps:
- Preprocessing source code in C): Comment removal, Macro Expansion, File includes, Conditional macros
- Compiling (Expanded source code): Converts from the intermediate file to Assembly files, this is where any errors or warnings are found and shown in the terminal
- Assembling (assembly code -> Object code): Assembly is then converted to binary using an assembler, this new binary file is called a object file
- Linking (Executable file): Last step is including “the library files” that contains the definitions of the function for the machine language, then generates an exe or out file to run.

Virtual Functions:
- Use to override function of a parent class, declare parent method as virtual
- No virtual function becomes a problem when using polymorphism 
- Implemented using a vtable 

Pure Virtual Function: Define a function inside of a parent class without an implementation and then have child classes actually implement it. Syntax is setting equal to 0. Interface: A class that consists of only unimplemented functions. Once a class is all pure virtual you can no longer insatiate it. 

Smart Pointers:
- Shared: Share ownership of a memory address so there can be many pointers pointing to it, for each new pointer it increments a num_pointers value, when they go out of scope a pointer is deleted and the num_pointers value is decremented, when it reaches 0 the pointer address is freed. 
- Unique: Wraps a pointer and deletes it when the instance of the pointer goes out of scope
- Weak: works with shared pointers but doesn't increase the reference count to stop cyclical bugs where a shared pointer points to another shared pointer. Actually increments a weak count also stored in the same memory block as the shared pointer. 

Invariants: A condition that must be true during the execution of a program. 
- Class invariants - A condition that must be true before and after every function call, it is checked in the constructor and in every public function. 
- Loop invariants - a condition that must be true at the start of each iteration
- Algorithm invariants - a check within an algorithm ie checking if an itr is within the bounds of an array

Encapsulation: Just the idea of putting the data initialization and functions into one thing, a class. So that a user can just black box and use what is necessary.

Abstraction(visibility): +Public(default for structs), # Protected, -Private(default for classes)
Inheritance: When child class inherits the functionality of a parent class. Implemented by: class childclass : public parentclass

Polymorphism: Having multiple types for a single type. 
- Static polymorphism (compile time) - When you use function and operator overloading 
- Dynamic Polymorphism(runtime) - When you use method overriding and virtual functions 

Operator Overloading:  Allows you to use +, -, > etc.. with user defined types like classes and structs. This is done by putting what kinda looks like another constructor, ex (class operator+(const class& other)) or like making a class act like an array. 

Function Overloading: When you have multiple function declarations in your class and depending on the params fed to the object, it calls a different function. 

namespaces: A way to group related identifiers (variables, functions, classes, objects) together to apparently avoid conflicts where the same function is defined multiple times. To use functions in a name space you have to use the scop resolution operator (::) or use the using keyword namespace in your file.

references: A way to create an alias for another variable. Supposedly makes it easier to use variables in functions without the "overhead of copying large objects". Syntax is to use the & symbol in the type.

Exceptions: A type of object that you can throw to the call stack, cool thing about exceptions is that if there is no try catch in the previous stack frame it will keep going back until main where it will return an error and end the program. "throw by value, catch by reference". If there is heap allocated memory when a throw goes through the call stack, there could be a memory leak.

Big Five: Special member function that defines how class manages memory allocation/deallocation & moving/copying objects.
- Destructor - gets automatically invoked when an object goes out of scope or is deleted. Deletes dynamically allocated resources. (~classname) 
- Copy Constructor (deep copy) - Creates a new object as a copy of an existed one. 
- Copy Assignment Operator (operator = (const className& other) - Assigns an existing object to another existing object. 
- Move Constructor - Moves resources instead of copying
- Move Assignment Operator - moves resources during assignment

const keyword: 
- makes a variable immutable after init
- const pointer can't be reassigned
- const member function so you cant modify member variables int func() const {}
- const object - you can only use the const functions declared in the class and only read member variables. You can set a member variable to the mutable keyword to be able to modify it in a const object.
- mutable keyword - changes the physical constness so the bits can be changed but the logical constness is the same so the object can be regarded as the same. 

static keyword
- local variable - retains value across the entire runtime regardless of scope
- global variables - limits scope of the variable to the file 
- member variable - shared by all instances of the class instead of being unique to each instance. It can also be called without an instance of the object at all. 
- function - limits scope of the function to the file 
- object - retains values between multiple function calls 
- class - Only static method and variables, you literally cant instantiate an object form it you have to just use the static functions and variables 

Modules: A new way to organize and manage code which replaces normal # include headers. Create a module using .cppm at the top put like export module mymodule;  and then your function declarations.  Then in your cpp put import mymodule; This stops the duplicate parsing of includes and ordering imports. 

Syntax/misc:
- I/O cin >>, cout <<, cerr
- int d, long ld, char c, float f, double lf
- iterator .begin(), .end() (element after last)
- reverse iterator .rbegin()
- Three way spaceship operator - automates comparisons between objects, interpret answer from the return value
- friend keyword - gives another class access to private 
- Nested Classes - you can nest classes, private & protected is only available to the outer class unless you use the friend key. ex tree
- abstract class - where one of the methods is pure virtual, a interface is an abstract class 
- object is an instance of a class, you can create a pointer to objects
- constructor - default is empty, can force user to give parameters
- destructor - default is hidden, necessary if dynamically allocating memory (~class name)
- virtual destructor - the one virtual method you have to implement in the class 
- struct  - default public but is technically no different with defining member variables but you cant encapsulate member functions inside it. Usually used for simpler data structures. 
- RAII (Resource Allocation Is Initialized) - Every resource should be wrapped in a stack allocated object who releases it
- explicit keyword - if you don't want implicit type conversions in your constructor, put after the params in the constructor definition 
- inline keyword - suggests tot he compiler to replace the function call with the actual block of code, used when the actual code for the function would take less compute than a function call overhead
- decorator - wrapping an object in another object which lets you dynamically modify and objects behavior, an alternative to subclasses. 
- MIL (member initialization list) - When you initialize your members in your constructor after the parameters but before the constructor body. Const and ref members must be initialized like this. Faster because there is no default initialization. 
- argc (number of args)/argv (array of char pointers to args) - how you take command line arguments into your main 
- noexcept keyword- any exceptions are handled inside the function and nothing is thrown, makes compilation faster 

Containers: A holder object that stores other objects, implemented as class templates. 
- Sequence Containers - Array, vector, list (doubly linked list), deque 
- Associative - Set, multiset, map, multimap (multi just means keys aren't unique)
- Unordered Associative - unordered set/multiset, unordered map/multimap
- Adapters (difference interface for sequential containers) - stack, queue, p queue

iterators: An object that allows you to traverse a vector, map, set without using underlying structure. It is a pointer to the object though so you have to do (* it) to get value. You can also ++ or -- to increment through. A reverse iterator is the same but backwards.

Coupling: Refers to the amount of dependency between different components (classes, modules, functions) of a program.

lambdas - An anonymous function that can be defined inline, basically lets you define small functions without creating a named function. [ capture ] ( parameters ) -> return_type { function_body }

static/dynamic binding: static is when things are defined and linked in compile time vs dynamic is runtime? you can use the virtual keyword to dynamically bind functions. 

Map (red black tree O(logn)) vs Unordered Map (hash table O(1) average): Both store data in key - value pairs, however, a map is sorted in ascending order and unordered map is not. 

Trees: Hierarchical data structure with nodes, each node contains a value and then a point to a child node which is recursive.

Questions:
1. Explain why C++ is called OOPs.
2. Explain polymorphism and its types in C++.
3. List the features of OOPs in C++.
4. What are ‘class’ and ‘object’ in C++?
5. What is a storage class used in C++?
6. What are encapsulation and inheritance in C++?
7. Name popular OOPs languages.
8. What are the main OOPs features?
9. Differentiate between class and structure? 
10. Differentiate between polymorphism and inheritance.
11. What is coupling?
12. What is structured programming?
13. What is the difference between a class and namespace?

```C++
#include <map>
class StockPrice {
private:
    unordered_map<int, int> stock; // timestamp, price
    multiset<int> prices;
    int max_time = 0;
public:
    StockPrice() { }
    void update(int timestamp, int price) {
        if (stock.count(timestamp)){
            auto it = prices.find(stock[timestamp]);
            prices.erase(it);
        }
        stock[timestamp] = price;
        prices.insert(price);
        max_time = max(max_time, timestamp);
    }
    int current() {
        return stock[max_time];
    }
    int maximum() {
        if (stock.empty())
            return 0;
        return *prices.rbegin();
    }
    int minimum() {
        if (stock.empty())
            return 0;
        return *prices.begin();
    }
};
```

```C++
class UndergroundSystem {
private:
    map<int, pair<string, int>> infomap; //id, station, time
    map<string, pair<int, int>> timemap; // (station1,station2), time taken, # trips
public:
    UndergroundSystem() {
    }
    void checkIn(int id, string stationName, int t) {
        if (infomap.count(id) > 0) {
        }
        else {
            infomap[id] = make_pair(stationName, t);
        }
    }
    void checkOut(int id, string stationName, int t) {
        auto info = infomap[id];
        infomap.erase(id);
        string path = info.first + ',' + stationName;
        int time = t - info.second;
        if (timemap.count(path) > 0){
            timemap[path].first += time;
            timemap[path].second++;
        }
        else{
            timemap[path] = make_pair(time, 1);
        }
    }

    double getAverageTime(string startStation, string endStation) {
        string path = startStation + ',' + endStation;
        auto timeinfo = timemap[path];
        return (double) timeinfo.first / timeinfo.second;
    }
};
```

```C++
#include <iostream>
#include <string>

class Animal {
private:
    int age = 0;
    std::string breed;

public:
    virtual void foo(int a, int b) = 0;  //  Pure virtual function
};

class Dog : public Animal {  // Correct inheritance
public:
    void foo(int a, int b) override {  // Correct override
        std::cout << "Dog's foo method called!" << std::endl;
    }
};

int main() {
    Dog dog1;  // Correct object instantiation
    dog1.foo(1, 2);  // Calls `Dog::foo`

    Animal* animal1 = &dog1;  // Pointer to `Dog`
    animal1->foo(1, 2);  // Calls overridden `Dog::foo` (Dynamic Binding)

    return 0;
}
```

```C++
#include <iostream>
#include <string>

class Animal {
private:
    int age = 0;
    std::string breed;

public:
	    void foo(int a, int b) { 
		    std::cout << "blank" << std::endl;
	    };  
};

class Dog : public Animal { 
public:
    void foo(int a, int b) {  
        std::cout << "Dog's foo method called!" << std::endl;
    }
};

int main() {
    Dog dog1; 
    dog1.foo(1, 2); 

    Animal* animal1;
	animal1 = &dog1; 
    animal1->foo(1, 2); 

    return 0;
}
```

