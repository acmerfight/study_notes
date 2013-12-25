#### A Tour of Computer Systems
*   All information in a system—including disk files, programs stored in memory, user data stored in memory, and data transferred across a network—is represented as a bunch of bits. The only thing that distinguishes different data objects is the context in which we view them. 

#### Representing and Manipulating Information
##### Information Storage
*   Rather than accessing individual bits in memory, most computers use blocks of eight bits, or bytes, as the smallest addressable unit of memory. A machine-level program views memory as a very large array of bytes, referred to as virtual memory. Every byte of memory is identified by a unique number, known as its address, and the set of all possible addresses is known as the virtual address space.As indicated by its name, this virtual address space is just a conceptual image presented to the machine-level program. The actual implementation uses a combination of random-access memory (RAM), disk storage,special hardware, and operating system software to provide the program with what appears to be a monolithic byte array.
*   Every computer has a word size, indicating the nominal size of integer and pointer data. Since a virtual address is encoded by such a word, the most important system
parameter determined by the word size is the maximum size of the virtual address space. That is, for a machine with a w-bit word size, the virtual addresses can range from 0 to 2 ** w − 1, giving the program access to at most 2w bytes.
*    

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
*   the least significant byte comes first is referred to as little endian. This convention is followed by most Intel-compatible machines. The latter convention—where the most significant byte comes first is referred to as big endian. This convention is followed by most machines from IBM and Sun Microsystems.
*   machines support two forms of right shift: logical and arithmetic. A logical right shift fills the left end with k zeros, giving a result [0, . . . , 0, xn−1, xn−2 , . . . xk ]. An arithmetic right shift fills the left end with k repetitions of the most significant bit, giving a result [xn−1, . . . , xn−1, xn−1, xn−2 , . . . xk ].This convention might seem peculiar, but as we will see it is useful for operating on signed integer data.

##### Integer Representations
*   Treating x as a number written in binary notation, we obtain the unsigned interpretation of x. We express this interpretation as a function B2Uw (for “binary to unsigned,” length w)

![](https://raw.github.com/acmerfight/study_notes/master/images/B2U.png)

![](https://raw.github.com/acmerfight/study_notes/master/images/uexample.png)
*   This is defined by interpreting the most significant bit of the word to have negative weight. We express this interpretation as a function B2Tw.The most significant bit xw−1 is also called the sign bit. Its “weight” is − 2w−1, the negation of its weight in an unsigned representation. When the sign bit is set to 1, the represented value is negative, and when set to 0 the value is nonnegative.

![](https://raw.github.com/acmerfight/study_notes/master/images/B2T.png)

![](https://raw.github.com/acmerfight/study_notes/master/images/2.png)
*   This relationship is useful for proving relationships between unsigned and two’s-complement arithmetic. In the two’s-complement representation of x, bit xw−1 determines whether or not x is negative, giving

![](https://raw.github.com/acmerfight/study_notes/master/images/T2U.png)

![](https://raw.github.com/acmerfight/study_notes/master/images/3.png)
*   To convert an unsigned number to a larger data type, we can simply add leading zeros to the representation; this operation is known as zero extension. For converting a two’s-complement number to a larger data type, the rule is to perform a sign extension,

##### Integer Arithmetic
*   unsigned addition

![](https://raw.github.com/acmerfight/study_notes/master/images/addu.png)

![](https://raw.github.com/acmerfight/study_notes/master/images/addu1.png)
*   Two’s-Complement Addition

![](https://raw.github.com/acmerfight/study_notes/master/images/adds.png)

![](https://raw.github.com/acmerfight/study_notes/master/images/adds1.png)
*   Unsigned Multiplication and Two’s-Complement Multiplication  
    (x * y) mod 2**w
*   On most machines, the integer multiply instruction is fairly slow, requiring 10 or more clock cycles, whereas other integer operations—such as addition, subtraction, bit-level operations, and shifting—require only 1 clock cycle. As a consequence, one important optimization used by compilers is to attempt to replace multiplications by constant factors with combinations of shift and addition operations.
*   Given that integer multiplication is much more costly than shifting and adding, many C compilers try to remove many cases where an integer is being multiplied by a constant with combinations of shifting, adding, and subtracting.
*   Integer division on most machines is even slower than integer multiplication requiring 30 or more clock cycles. Dividing by a power of 2 can also be performed using shift operations, but we use a right shift rather than a left shift. The two different shifts—logical and arithmetic—serve this purpose for unsigned and two’s-complement numbers, respectively.

##### Floating Point
*   The symbol ‘.’ now becomes a binary point, with bits on the left being weighted by positive powers of 2, and those on the right being weighted by negative powers of 2. For example, 101.112 represents the number 1 × 2**2 + 0 × 2*1 + 1 × 2*0 + 1 × 2**−1 + 1 × 2**−2 = 4 + 0 + 1 + 2 + 4 = 5+3/4

![](https://raw.github.com/acmerfight/study_notes/master/images/f1.png)

![](https://raw.github.com/acmerfight/study_notes/master/images/f2.png)
*   The IEEE floating-point standard represents a number in a form V = (−1) pow s × M × 2 pow E:
    *   The sign s determines whether the number is negative (s = 1) or positive
        (s = 0), where the interpretation of the sign bit for numeric value 0 is handled
        as a special case.
    *   The significand M is a fractional binary number that ranges either between 1 and 2 − e or between 0 and 1 − e.
    *   The exponent E weights the value by a (possibly negative) power of 2.

*   The bit representation of a floating-point number is divided into three fields to encode these values:
    *   The single sign bit s directly encodes the sign s.
    *   The k-bit exponent field exp = ek−1 . . . e1e0 encodes the exponent E
    *   The n-bit fraction field frac = fn−1 . . . f1f0 encodes the significand M, but the value encoded also depends on whether or not the exponent field equals 0.
    *   ![](https://raw.github.com/acmerfight/study_notes/master/images/f3.png)

*   

    ![](https://raw.github.com/acmerfight/study_notes/master/images/f4.png)



