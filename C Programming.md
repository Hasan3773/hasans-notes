Macro definitions, Ternary Operator,  inline operators*, #error, 
Infinite loop while(1) or for(;;) - K&R preferred method
*- pointer lol
& - references some shit
  
Big Endian: Stores the MSB first
Little Endian: Stores the LSB first
  
Declarations:
(a) int a; // An integer
(b) int *a; // A pointer to an integer
(c) int **a; // A pointer to a pointer to an integer
(d) int a[10]; // An array of 10 integers
(e) int *a[10]; // An array of 10 pointers to integers
(f) int (*a)[10]; // A pointer to an array of 10 integers
(g) int (*a)(int); // A pointer to a function a that takes an integer argument and returns an integer
(h) int (*a[10])(int); // An array of 10 pointers to functions that take an integer argument and return integer

static Keyword - Initialized to the scope of the file and cant be referenced outside that file, If initialized in a function, it exists before and after the func call.
Const Keyword - Read Only, 
const int a; - Constant integer
int const a; - Constant integer
const int *a; - pointer to a constant integer
int * const a; - constant pointer to an integer
int const * a const; - constant pointer to a constant integer

Volatile Keyword - Tells the compiler that its value can change at any point so it should not make any assumptions of its value. Uses: Hardware registers(ie Status register), multi threading, ISRs,  Real time systems, dynamic memory allocation
Can a variable be both const and volatile? - Yes for example a read only status reg
Can a pointer be volatile? -Yes but not many uses, one is an ISR switching which data buffer its pointing to
  
Inline Functions: Inline is basically a suggestion to the compiler that it can replace the function call with the code from the function itself to reduce overhead costs associated with function calls. 
  
Compilation steps in C: Process of turning user code to machine code
- Preprocessing (source code in C): Comment removal, Macro Expansion, File includes, Conditional macros
- Compiling (Expanded source code): Converts from the intermediate file to Assembly files, this is where any errors or warnings are found and shown in the terminal
- Assembling (assembly code -> Object code): Assembly is then converted to binary using an assembler, this new binary file is called a object file
- Linking (Executable file): Last step is including “the library files” that contains the definitions of the function for the machine language, then generates an exe or out file to run.
--
Data Types:
- int: 16-bit signed number
- long: 
- float: 32-bit unsigned adds 7 sig figs
- double: double the length of a float
- char: a single byte

Printf:
- %6.1 print with length 6 chars and to 1 decimal point
- %f: print as floating point / double
- %d print as decimal int
- %ld print as long int
- %o print as octal
- %x print as hexadecimal
- %c print as character
- %s print as string

Increment Operators:       

```C
```cpp
    int getSum(int a, int b) {
        // The goal is to get the sum of two integers without using + or -
        // basically asking to implement algo that uses bitwise to do sum
        // lets say we have 0001 + 0010, which is 1 + 2, the | operator would work to 0011
        // but lets say 0011 + 0010, | would give us 0010
        // Idea lets for loop through each of the ints, adding the right most bit, then 
        // right shifting, I think we might be able to carry ones 
        int mask = 0x1;
        int round = 1;
        int num = 0;
        int carry = 0;

        for (int i = 0; i < sizeof(int)*8; i++){ // 32 bits in an int
            // mask a & b to get the LSB of each
            int bitA = a & mask;
            int bitB = b & mask;
            // calcs the sum of the two nums using xor
            int sum = bitA ^ bitB;
            // takes into acount the carry to the sum
            sum ^= carry;
            // calculates the carry for the next bit by 
            // by checking the case where a & b are 1 and
            // the case where 1 or the other is 1 and there is a carry 
            carry = (bitA & bitB) | (carry & (bitA ^ bitB));
            // adds the bit specifc sum to the overall sum
            num |= (sum << i);
            // right shifts for next bit
            a >>= 1;
            b >>= 1;
        }
        return num;

		uint32_t ones = 0;
	    while(n != 0){
	        n = n & n-1;
	        ones++;
	    }
	    return ones;
```