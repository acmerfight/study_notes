#### A Tour of Computer Systems
1.  All information in a system—including disk files, programs stored in memory, user data stored in memory, and data transferred across a network—is represented as a bunch of bits. The only thing that distinguishes different data objects is the context in which we view them. 

#### Representing and Manipulating Information
##### Information Storage
1. Rather than accessing individual bits in memory, most computers use blocks of eight bits, or bytes, as the smallest addressable unit of memory. A machine-level program views memory as a very large array of bytes, referred to as virtual memory. Every byte of memory is identified by a unique number, known as its address, and the set of all possible addresses is known as the virtual address space.As indicated by its name, this virtual address space is just a conceptual image presented to the machine-level program. The actual implementation uses a combination of random-access memory (RAM), disk storage,special hardware, and operating system software to provide the program with what appears to be a monolithic byte array.
2.  Every computer has a word size, indicating the nominal size of integer and pointer data. Since a virtual address is encoded by such a word, the most important system
parameter determined by the word size is the maximum size of the virtual address space. That is, for a machine with a w-bit word size, the virtual addresses can range from 0 to 2 ** w − 1, giving the program access to at most 2w bytes.
3.  

C declaration|32-bit|64-bit
:---------------|:---------------|:---------------
char|1|1
short int|2|2
int|4|4
long int|4|8
long long int|8|8
char *|4|8
float|4|4
double|8|8

4.  the least significant byte comes first is referred to as little endian. This convention is followed by most Intel-compatible machines. The latter convention—where the most significant byte comes first is referred to as big endian. This convention is followed by most machines from IBM and Sun Microsystems.
5.  machines support two forms of right shift: logical and arithmetic. A logical right shift fills the left end with k zeros, giving a result [0, . . . , 0, xn−1, xn−2 , . . . xk ]. An arithmetic right shift fills the left end with k repetitions of the most significant bit, giving a result [xn−1, . . . , xn−1, xn−1, xn−2 , . . . xk ].This convention might seem peculiar, but as we will see it is useful for operating on signed integer data.

##### Integer Representations
1.  Treating x as a number written in binary notation, we obtain the unsigned interpretation of x. We express this interpretation as a function B2Uw (for “binary to unsigned,” length w)

![](https://raw.github.com/acmerfight/study_notes/master/images/B2U.png)

![](https://raw.github.com/acmerfight/study_notes/master/images/uexample.png)

2.  This is defined by interpreting the most significant bit of the word to have negative weight. We express this interpretation as a function B2Tw.The most significant bit xw−1 is also called the sign bit. Its “weight” is − 2w−1, the negation of its weight in an unsigned representation. When the sign bit is set to 1, the represented value is negative, and when set to 0 the value is nonnegative.

![](https://raw.github.com/acmerfight/study_notes/master/images/B2T.png)

![](https://raw.github.com/acmerfight/study_notes/master/images/2.png)


