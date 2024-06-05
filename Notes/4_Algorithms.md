### Big O Notation
***

![Big O Notation](../images/BigONotation.png)

#### Static Arrays
***


| Operation | Big O Time | Notes                                                                 |
|-----------|------------|-----------------------------------------------------------------------|
| Reading   | O(1)       | Reading an element by index is constant time.                         |
| Insertion | O(n)*      | Insertion at the end of the array 'push( )' is typically O(1) on average. However, resizing may occasionally lead to O(n) time complexity. |
| Deletion  | O(n)*      | Deletion from the end of the array 'pop( )' is typically O(1) on average. However, resizing may occasionally lead to O(n) time complexity. |

#### Dynamic Arrays (Python Lists)
***

| Operation | Big O Time | Notes                                                                                           |
|-----------|------------|-------------------------------------------------------------------------------------------------|
| Reading   | O(1)       | Reading an element by index is constant time, similar to regular arrays.                         |
| Insertion | O(1)*      | Insertion at the end of the list ('append()' operation) is typically O(1) on average. However, inserting in the middle requires shifting, leading to O(n) time complexity. |
| Deletion  | O(1)*      | Deletion from the end of the list ('pop()' operation) is typically O(1) on average. However, deleting from the middle requires shifting, leading to O(n) time complexity. |

**Notes**: Insertion and deletion at the end of a Python list (using methods like 'append()' and 'pop()') are also usually O(1) because Python dynamically manages memory for the list and avoids resizing the array too often. However, as mentioned in the notes, if insertion or deletion happens in the middle of the list, it requires shifting elements, resulting in an O(n) time complexity due to the need to move subsequent elements.

#### Stacks
***

| Operation | Big O Time | Notes                                                                                           |
|-----------|------------|-------------------------------------------------------------------------------------------------|
| Push      | O(1)       |                                                                                                 |
| Pop       | O(1)*      | Check if the stack is empty first.                                                              |
| Peek/Top  | O(1)*      | Retrieves without removing.                                                                     |

#### Linked Lists (1 Direction)
***

| Operation | Big O Time | Notes                                                     |
|-----------|------------|-----------------------------------------------------------|
| Access    | O(n)       |                                                           |
| Search    | O(n)*      |                                                           |
| Insertion | O(1)*      | Assuming you have the reference to the desired position.  |
| Deletion  | O(1)*      | Assuming you have the reference to the desired position.  |

#### Linked List (2 Directions)
***

| Operation | Big O Time | Notes                                                     |
|-----------|------------|-----------------------------------------------------------|
| Access    | O(n)       |                                                           |
| Search    | O(n)*      |                                                           |
| Insertion | O(1)*      | Assuming you have the reference to the desired position.  |
| Deletion  | O(1)*      | Assuming you have the reference to the desired position.  |

#### Queues
***


| Operation | Big O Time | Notes                                                     |
|-----------|------------|-----------------------------------------------------------|
| Enqueue   | O(1)       |                                                           |
| Dequeue   |  O(1)      |                                                           |

#### Binary Trees
***

| Operation       | Big O Time | Notes                                              |
|-----------------|------------|----------------------------------------------------|
| Search          | O(log n)   | Depends on the height of the binary tree           |
| Insertion       | O(log n)   | Depends on the height of the binary tree           |
| Deletion        | O(log n)   | Depends on the height of the binary tree           |
| Traversal       | O(n)       | In-order, Pre-order, Post-order traversals         |
| Finding height  | O(n)       | Worst case if the tree is unbalanced               |
| Finding depth   | O(n)       | Worst case if the tree is unbalanced               |
| Finding minimum | O(log n)   | Traverse left until you reach the leftmost leaf    |
| Finding maximum | O(log n)   | Traverse right until you reach the rightmost leaf  |

#### Heaps
***

| Operation        | Big O Time | Notes                                       |
|------------------|------------|---------------------------------------------|
| Insertion        | O(log n)   | Heapify up operation                        |
| Deletion (Root)  | O(log n)   | Heapify down operation                      |
| Search           | O(n)       | Linear search through the array             |
| Extract Minimum  | O(log n)   | Removal of the root followed by heapify down |
| Extract Maximum  | O(log n)   | Removal of the root followed by heapify down |
| Peek Minimum     | O(1)       | Accessing the root                           |
| Peek Maximum     | O(1)       | Accessing the root                           |
| Heapify          | O(n)       | Building a heap from an unsorted array       |
| Merge            | O(n log n) | Building a new heap from two existing heaps  |

#### Hashmaps
***

| Operation       | Average Case | Worst Case  | Notes                                               |
|-----------------|--------------|-------------|-----------------------------------------------------|
| Insertion       | O(1)         | O(n)        | Depends on load factor and collision resolution    |
| Deletion        | O(1)         | O(n)        | Depends on load factor and collision resolution    |
| Search          | O(1)         | O(n)        | Depends on load factor and collision resolution    |
| Access          | O(1)         | O(n)        | Depends on load factor and collision resolution    |
| Collision Avoid.| -            | O(n)        | Depends on implementation and hashing algorithm    |
| Rehashing       | O(n)         | O(n)        | Depends on the number of elements and load factor  |




#### Sorting algorithms
***

| Algorithm    | &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Time Complexity  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| Space Complexity |
|--------------|--------------------------------------------|------------------|

|                | Best       | Average    | Worst      | Worst            |
|----------------|------------|------------|------------|------------------|
| Mergesort      | O(n log n) | O(n log n) | O(n log n) | O(n)             |
| Quicksort      | O(n log n) | O(n log n) | O(n^2)     | O(log n) - O(n)  |
| Insertion Sort | O(n)       | O(n^2)     | O(n^2)     | O(1)             |
| Bucket Sort    | O(n+k)     | O(n+k)     | O(n^2)     | O(n)             |
