#### 计算机系统漫游
    All information in a system—including disk files, programs stored in memory, user data stored in
    memory, and data transferred across a network—is represented as a bunch of bits.
    The only thing that distinguishes different data objects is the context in which
    we view them. 
#### 信息的表示和处理
    Rather than accessing individual bits in memory, most computers use blocks
    of eight bits, or bytes, as the smallest addressable unit of memory. A machine-
    level program views memory as a very large array of bytes, referred to as virtual
    memory. Every byte of memory is identified by a unique number, known as its
    address, and the set of all possible addresses is known as the virtual address space.
    As indicated by its name, this virtual address space is just a conceptual image
    presented to the machine-level program. The actual implementation (presented
    in Chapter 9) uses a combination of random-access memory (RAM), disk storage,
    special hardware, and operating system software to provide the program with what
    appears to be a monolithic byte array.

