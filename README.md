# Data Structures and Algorithms Notes

Personal notes for the course of Neetcode - Data Structures and Algorithms for Beginners

## 02 - Arrays

### RAM

- RAM (Random Access Memory) is where variables are stored.
- Arrays are stored in RAM in bytes.
- A byte is 8 bits, where a bit is a 0 or 1.
- Integers are represented by 4 bytes.  
  Assuming we have 32 bits (4 bytes * 8 bits), an integer 1 will be represented as zeros until the LSB, which will be 1. Then we will put it into the RAM.
- Every value is stored in an address. We don't always get to choose the location, but it will be continuous (nothing will be in-between). Every address will jump by 4 as each value takes 4 bytes to store.

We can store chars as well, continuously, but the address will jump by 1 as each char takes only 1 byte in memory for ASCII chars.

## Static Arrays

Let's assume we have an array: `myArray = [1, 3, 5]`.  
To read the first element, we go to the address and read it from there; at least that's what happens under the hood. We don't need to know the address of every value; we use indexes to access the values. The first value is at index 0, the next at 1, and so on. Since we can map any index to a location in memory, we can instantly read any value as long as we have the index for it. To represent that as an efficient operation, we call it **O(1)**. In the worst case, assuming we have the value, it's an instant operation, happening in constant time. No matter how big the array is, we can read the value instantly.

- RAM allows us to instantly access the data in memory.  
- We can iterate through the indexes of the array using a for loop.

Until now, we have spoken about reading. Now let's talk about writing.  
Suppose we have a fixed-size array, so it would still be continuous. We don't always get to decide where we store our values. If we try to access an index after the assigned array, we don't know what comes after the final address of the array. It might be used (for static arrays).  
Some programming languages use **dynamic arrays** as the default, which is why you might not have encountered such limitations.  
- We can't remove a value from a static array; we can only overwrite it with 0, making it no longer relevant.
- Writing a new value is also an **O(1)** operation.  
- Removing (overwriting) a value is also **O(1)**.  
- Inserting at the end of an array is an efficient operation, which again is **O(1)**, but if we want to insert a value in the middle or start of the array, it won't be efficient because we have to shift the other values to other positions.

Example: `myArray = [5, 6, 0]`, and we want to insert 4 at the start. We will have to move `myArray[1]` to `myArray[2]`, `myArray[0]` to `myArray[1]`, and then overwrite `myArray[0]` with 4. This is not done in a single operation, and in a really long array, we would have to shift all these values just to insert one value. It's not efficient. This is called **O(n)**, where `n` refers to the length of the array. In the worst-case scenario, if you insert a value, you might have to shift all `n` values.

- The same principle applies to shifting left and removing an MSB.

| Operation         | Big-O Time |
|-------------------|------------|
| Read/Write i-th element | O(1)       |
| Insert/Remove end       | O(1)       |
| Insert middle           | O(n)       |
| Remove middle           | O(n)       |

## Dynamic Arrays

Dynamic arrays are much more common and useful than static arrays. They are used in Python and Java by default. In C++, it's called a vector.

- For static arrays, we had to initialize the length of the array, but in a dynamic array, you don't have to specify the size. It will be initialized with a default size, but the length of the array will be 0, as nothing was added to it.  
- Adding elements to the array is called pushing values into the array. It will maintain a pointer that will tell us what is the last element of the array, the index. We can also use the pointer to get the length. 
- We can also pop values, which also refers to the end of the array. Just like pushing a value is **O(1)**, so is popping **O(1)**, as we know where the value is thanks to the pointer. After popping, the pointer will shift left and will point to the new end of our array. If we pop everything, the length will be 0.  
- If we push another value after reaching our size limit, we will run out of space, so our dynamic array will allocate a new array that will be able to contain the elements we are trying to store.  
- After allocating a new array, it will go somewhere random in the memory, but we don't really care where it goes. We will take all the original values and copy them into the second array starting at the beginning. Then, we de-allocate the original array as we do not need it anymore, to free up memory. If we run out of space again, we will allocate a new array which is double the original size.  

### Why Double the Size of the Array?

Since we allocated a new array, we did an **O(n)** operation where `n` is the size of the array. We also had to push all the original values to the new array, which is also **O(n)**. If we run out of space, we can create a new array, but it takes extra time as we create a new array and push the new values again. That's why when we create a bigger array, we double the capacity and not increase it by 1, so we find a middle ground and won't create a new array every single time. We could also make a huge array with a lot of empty space, but then it takes up all of our memory.  

### Amortized Complexity

When we do so, we get **Amortized Complexity**, which means yes, it took **O(n)** to add an element if we run out of space, but we know it will be infrequent. So we can say the amortized time complexity of pushing a value will be **O(1)**. On average, it will be **O(1)**, not **O(n)**. This can be proven by the power series.

### Mathematical Proof

To understand the amortized time complexity, consider the cost of inserting elements into a dynamic array that doubles in size whenever it runs out of space. Let's denote:

- \( n \) as the number of elements inserted.
- The initial capacity of the array is 1 (it will grow to 1, 2, 4, 8, ...).

The total cost \( T(n) \) of inserting \( n \) elements includes both the copying of elements to a new array when resizing and the insertion of new elements. 

Each time the array is resized, we double its capacity. The number of times we resize the array is \( \log_2 n \) because we double the capacity each time.

The cost for inserting the elements can be broken down as follows:
- Inserting elements without resizing: \( O(1) \) per insertion.
- Resizing: The cost of copying elements when the array is resized.

When the array size reaches \( 2^k \) (for some integer \( k \)):

- Inserting the first \( 2^k \) elements has a copying cost of \( 0 + 1 + 2 + 4 + \ldots + 2^{k-1} \), which is the sum of a geometric series.

The total cost for inserting \( n \) elements, where \( n \) is a power of 2:
\[ T(n) = \sum_{i=0}^{\log_2 n} 2^i = 2^{\log_2 n + 1} - 1 = 2n - 1 \]

Thus, the average cost per insertion (amortized cost) is:
\[ \frac{T(n)}{n} = \frac{2n - 1}{n} = 2 - \frac{1}{n} \]

As \( n \) becomes large, \( \frac{1}{n} \) approaches 0, so the amortized cost is:
\[ O(1) \]



### Big-O Time Complexity

In **O(n)** time complexity, we don't really care about the constants in the parenthesis as it grows linearly. If it was **O(n^2)** (quadratic complexity), it would add way more complexity. We don't care about addition or multiplication of constants. For smaller inputs, it might matter. We care about big input sizes as those slow our CPUs down when we run the programs.  

If we add a constant compared to \( n^2 \), at some point, the complexity will intersect, and it will grow way faster while the linear one will grow

## Stacks

Stacks support these three operations:

| Operation  | Big-O Time |
|------------|------------|
| Push       | O(1)       |
| Pop        | O(1)       |
| Peek/Top   | O(1)       |

- Dynamic arrays satisfy all these requirements, so a stack can be implemented using a dynamic array.
- We can push elements into the array, which is the end of the stack, and a pointer will indicate the location.
- Stacks are an example of the usage of dynamic arrays.
- The last element added is the first element that will be removed, similar to a magazine.
- Stacks are LIFO (Last In, First Out) data structures.
- We can use a stack to reverse an array. For example, turn `myArray = [3, 4, 5]` into `myArray = [5, 4, 3]` by popping its elements and pushing them into a new array.

## 03 - Linked lists
