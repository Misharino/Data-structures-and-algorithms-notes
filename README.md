# Data-structures-and-algorithms-notes
personal notes for the course of neetcodee - data structures and algorithms for beginners
## 0.2 - Arrays
### RAM
* RAM (Random access memory) is where variables are stored.
* Arrays will be stored in RAM in bytes. 
* A byte is 8 bits, where bit is a 0 or 1.
* Intergers are represented by 4 bytes.
Assuming we have 32 bits, (4 bytes * 8 bits) int 1 will be represeted as zeros until the LSB, which will be 1. Then we will put it into the RAM.
* Every value will be stored in an adress. We dont always get to choose the location, but it will be continuous (nothing will be in-between). Every adress will jump by 4 as each value takes 4 bytes to store.
We can store chars as well, continuously but the adress will jump by 1 as each char takes only 1 byte in memmory, for ASCII chars.
