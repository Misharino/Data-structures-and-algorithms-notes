# Data-structures-and-algorithms-notes
Personal notes for the course of neetcodee - data structures and algorithms for beginners
## 02 - Arrays
### RAM
* RAM (Random access memory) is where variables are stored.
* Arrays will be stored in RAM in bytes. 
* A byte is 8 bits, where bit is a 0 or 1.
* Intergers are represented by 4 bytes.  
Assuming we have 32 bits, (4 bytes * 8 bits) int 1 will be represeted as zeros until the LSB, which will be 1. Then we will put it into the RAM.
* Every value will be stored in an adress. We dont always get to choose the location, but it will be continuous (nothing will be in-between). Every adress will jump by 4 as each value takes 4 bytes to store.  
We can store chars as well, continuously but the adress will jump by 1 as each char takes only 1 byte in memory, for ASCII chars.


## Static arrays
Lets assume we have an array: myArray [1,3,5].
To read the first element we will go to the adress and read it from there, at least thats what happens under the hood. We dont need to know the adress of every val, we use indexes to access the values. First value at index 0, next at 1 and 2, ex. Since we can map any index to a location in memory, we can instantly read any val as long as we have the index for it. To represent thats an efficient operation, we call it O(1). In worst case, assuming we have the value, its an instant operation, happens in constant time. No matter how big the array is, we can read the value instantly.  
* RAM - we can instantly access the data in the memory.  
* We can go through the indexes of the array using a for loop.  
Untill now we spoken about reading. Now lets talk about writing.  
Suppose we have a fixed size array, so it would be still continuous. We dont always get to decide where we store our values. If we try and access an index after the assigned array, we dont know what comes after the final adress of the array. It might be used (for static arrays).  
Some programming languages use **Dynamic arrays** as the default, thats why you might have not encountered yet such limitations.  
* We cant remove a value from a static array, we just can overwrite it with 0, and is no longer relevant.
* Writing a new value is also O(1) operation.  
* Removing (overwriting) a value is also O(1).  
* Inserting at the end of an array is an efficient operation, which again is O(1), but if we want to insert a value in the middle or start of the array, it wont be efficient, because we have to shift the other values to other positions.  
Example: myArray = [5,6,0], we want to insert 4 into the start. We will have to move myArray[1] -> myArray[2], myArray[0] -> myArray[1] and then overwrite myArray[0] with 4. This is not done in a single operation, which in a really long array we would have to shift all these values just to insert one value. Its not efficient. Its called **O(n)**, n reffers to a var, which is the length of the array. Worst case scenario, if you insert any value you might have to shift every value, n values.  
* Same thing goes to shifting left, removing a MSB.  

| Operation         | Big-O time |
|-------------------|------------|
| r/w i-th element  | O(1)       |
| Insert/remove end | O(1)       |
| Insert middle     | O(n)       |
| Remove middle     | O(n)       |


## Dynamic arrays