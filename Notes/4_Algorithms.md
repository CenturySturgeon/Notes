### Big O Notation
***

![Big O Notation](../images/BigONotation.png)

#### Static Arrays
***

| Operation | Big-O Time | Notes                                                                                                                                      |
|-----------|------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Reading   | O(1)       | Reading an element by index is constant time.                                                                                              |
| Insertion | O(n)*      | Insertion at the end of the array 'push( )' is typically O(1) on average. However, resizing may occasionally lead to O(n) time complexity. |
| Deletion  | O(n)*      | Deletion from the end of the array 'pop( )' is typically O(1) on average. However, resizing may occasionally lead to O(n) time complexity. |


#### Dynamic Arrays (Python Lists)
***

| Operation | Big-O Time | Notes                                                                                                                                                                      |
|-----------|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reading   | O(1)       | Reading an element by index is constant time, similar to regular arrays.                                                                                                   |
| Insertion | O(1)*      | Insertion at the end of the list ('append()' operation) is typically O(1) on average. However, inserting in the middle requires shifting, leading to O(n) time complexity. |
| Deletion  | O(1)*      | Deletion from the end of the list ('pop()' operation) is typically O(1) on average. However, deleting from the middle requires shifting, leading to O(n) time complexity.  |


**Notes**: Insertion and deletion at the end of a Python list (using methods like 'append()' and 'pop()') are also usually O(1) because Python dynamically manages memory for the list and avoids resizing the array too often. However, as mentioned in the notes, if insertion or deletion happens in the middle of the list, it requires shifting elements, resulting in an O(n) time complexity due to the need to move subsequent elements.

#### Stacks
***

| Operation | Big-O Time | Notes                                                                                           |
|-----------|------------|-------------------------------------------------------------------------------------------------|
| Push      | O(1)       |                                                                                                 |
| Pop       | O(1)*      | Check if the stack is empty first.                                                              |
| Peek/Top  | O(1)*      | Retrieves without removing.                                                                     |

#### Linked Lists (1 Direction)
***

| Operation | Big-O Time | Notes                                                     |
|-----------|------------|-----------------------------------------------------------|
| Access    | O(n)       |                                                           |
| Search    | O(n)*      |                                                           |
| Insertion | O(1)*      | Assuming you have the reference to the desired position.  |
| Deletion  | O(1)*      | Assuming you have the reference to the desired position.  |

#### Linked List (2 Directions)
***

| Operation | Big-O Time | Notes                                                     |
|-----------|------------|-----------------------------------------------------------|
| Access    | O(n)       |                                                           |
| Search    | O(n)*      |                                                           |
| Insertion | O(1)*      | Assuming you have the reference to the desired position.  |
| Deletion  | O(1)*      | Assuming you have the reference to the desired position.  |

#### Queues
***


| Operation | Big-O Time | Notes                                                     |
|-----------|------------|-----------------------------------------------------------|
| Enqueue   | O(1)       |                                                           |
| Dequeue   |  O(1)      |                                                           |

#### Binary Trees
***

| Operation       | Big-O Time | Notes                                              |
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

| Operation       | Big-O Time | Notes                                        |
|-----------------|------------|----------------------------------------------|
| Insertion       | O(log n)   | Heapify up operation                         |
| Deletion (Root) | O(log n)   | Heapify down operation                       |
| Search          | O(n)       | Linear search through the array              |
| Extract Minimum | O(log n)   | Removal of the root followed by heapify down |
| Extract Maximum | O(log n)   | Removal of the root followed by heapify down |
| Peek Minimum    | O(1)       | Accessing the root                           |
| Peek Maximum    | O(1)       | Accessing the root                           |
| Heapify         | O(n)       | Building a heap from an unsorted array       |
| Merge           | O(n log n) | Building a new heap from two existing heaps  |


#### Hashmaps
***

| Operation        | Average Case | Worst Case | Notes                                             |
|------------------|--------------|------------|---------------------------------------------------|
| Insertion        | O(1)         | O(n)       | Depends on load factor and collision resolution   |
| Deletion         | O(1)         | O(n)       | Depends on load factor and collision resolution   |
| Search           | O(1)         | O(n)       | Depends on load factor and collision resolution   |
| Access           | O(1)         | O(n)       | Depends on load factor and collision resolution   |
| Collision Avoid. | -            | O(n)       | Depends on implementation and hashing algorithm   |
| Rehashing        | O(n)         | O(n)       | Depends on the number of elements and load factor |




#### Sorting algorithms
***

| Algorithm    | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Time Complexity  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Space Complexity |
|--------------|--------------------------------------------s|------------------|

|                | Best       | Average    | Worst      | Worst            |
|----------------|------------|------------|------------|------------------|
| Mergesort      | O(n log n) | O(n log n) | O(n log n) | O(n)             |
| Quicksort      | O(n log n) | O(n log n) | O(n^2)     | O(log n) - O(n)  |
| Insertion Sort | O(n)       | O(n^2)     | O(n^2)     | O(1)             |
| Bucket Sort    | O(n+k)     | O(n+k)     | O(n^2)     | O(n)             |


### Handy Algorithms

- Listing All Contiguous Subarrays
    - A contiguous subarray is a sequence of elements that come from a larger array, and all elements in this subarray are adjacent to each other in the original array.

    ```Python
    test_str = '1234'
    ans = []

    # Go through all the numbers
    for i in range(len(test_str)):
        # Go through all the numbers beggining from i. 
        # Note that 'len(test_str) + 1' is due to slices not being inclusive on the right number.
        for j in range(i + 1, len(test_str) + 1):
            sub = test_str[i: j]
            ans.append(sub)

    # ['1', '12', '123', '1234', '2', '23', '234', '3', '34', '4']
    print(ans)
    ```

### Core Concepts

---

#### Multithreading vs. Multiprocessing

Multithreading and multiprocessing are both techniques for parallel execution, but they handle tasks and resources differently. Here’s a breakdown of their key differences:

##### Multithreading

1. **Concept**: Involves multiple threads within a single process. Threads share the same memory space and resources of the process, allowing easier and more efficient communication.

2. **Memory**: Threads within the same process share the same memory space, which can lead to data consistency issues and requires careful synchronization to avoid conflicts.

3. **Overhead**: Creating and managing threads generally involves less overhead compared to processes, as threads share the same memory and resources. Context switching between threads is typically faster.

4. **Concurrency**: Suitable for I/O-bound tasks or those requiring a lot of shared state. Threads can quickly exchange data and perform tasks dependent on shared resources.

5. **Limitations**: In languages like Python, threads are affected by the Global Interpreter Lock (GIL), limiting their effectiveness for CPU-bound tasks. Python threads are not truly parallel for CPU-intensive computations.

6. **Example Use Case**: Running multiple tasks concurrently, such as handling multiple user requests on a web server, or performing background tasks like updating a user interface.

##### Multiprocessing

1. **Concept**: Involves multiple processes, each with its own memory space and resources. Processes run independently and do not share memory space.

2. **Memory**: Each process has its own memory space, which eliminates the risk of data corruption from shared memory. However, processes need explicit mechanisms to communicate, such as inter-process communication (IPC) mechanisms like pipes or queues.

3. **Overhead**: Creating and managing processes has more overhead compared to threads, as each process has its own memory and resources. Context switching between processes is generally more expensive.

4. **Concurrency**: Suitable for CPU-bound tasks where you want to leverage multiple CPU cores for parallel computation. Processes run independently, eliminating resource contention.

5. **Limitations**: Communication between processes can be more complex and slower than between threads due to the need for IPC. Multiprocessing can also use more memory due to separate memory spaces for each process.

6. **Example Use Case**: Performing heavy computations that can be parallelized, such as processing large datasets, running simulations, or performing complex calculations.

## Summary

- **Multithreading** is ideal for tasks that need concurrent operations with shared state or resources, and is most effective for I/O-bound tasks or those requiring frequent thread communication.
- **Multiprocessing** is better suited for CPU-bound tasks that can be parallelized across multiple processors or cores, without the need for shared state.


# Saved for later

# Got-Stuck Problems

[241 Different Ways To Add Parentheses](https://leetcode.com/problems/different-ways-to-add-parentheses/description/)
    - [Explanation](https://leetcode.com/problems/different-ways-to-add-parentheses/solutions/5806448/beats-90-beginner-friendly-python3-java-c-c-rust-go-js)

[214 Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/description/)
    - [Explanation](https://www.youtube.com/watch?v=niOT-FK1RH8)

[440 Kth Smallest In Lexicographical Order](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/)
    - [Explanation](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/solutions/5818614/beats-100-easy-solution/)

#### Prefix Sum with Dictionary
https://leetcode.com/problems/continuous-subarray-sum/solutions/5276981/prefix-sum-hashmap-patterns-7-problems


[Leetcode Strategy Hustle](https://leetcode.com/discuss/study-guide/5762077/lld-strategy-hustle)

[Greedy Algorithm Guide](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/solutions/4836121/simple-beginner-friendly-dry-run-greedy-approach-readable-sol-time-o-n-space-o-1-gits)

# Solved Premium Problems

[Get Premium Probelms Here](https://interview-prep-pro.vercel.app)

- [490 The Maze](https://leetcode.ca/2017-04-03-490-The-Maze/)

    ```Python
    """
        There is a ball in a maze with empty spaces (represented as 0) and walls (represented as 1). The ball can go through the empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

        Given the m x n maze, the ball's start position and the destination, where start = [startrow, startcol] and destination = [destinationrow, destinationcol], return true if the ball can stop at the destination, otherwise return false.

        You may assume that the borders of the maze are all walls (see examples).
        """

        from typing import List
        import unittest

        class Solution:
            def canStopAtTarget(self, maze: List[List[int]], start: List[int], destination: List[int]):        
                rows, columns = len(maze), len(maze[0])
                directions = [(0, -1), (1, 0), (0, 1), (-1, 0)]
                visiting = set()
                dead_ends = set()
                print(destination)

                def dfs(row, column, depth):
                    visiting.add((row, column))
                    r, c = row, column

                    if (row, column) == (destination[0], destination[1]):
                        return True
                    if (row, column) in dead_ends:
                        return False
                    
                    # 4 rotations
                    for delta_row, delta_column in directions:
                        r, c = row, column
                        while 0 <= r + delta_row < rows and 0 <= c + delta_column < columns and maze[r + delta_row][c + delta_column] != 1:
                            r += delta_row
                            c += delta_column
                        if (r, c) not in visiting and dfs(r, c, depth + 1):
                            return True
                    
                    dead_ends.add((row, column))
                    visiting.remove((row, column))
                    return False

                return dfs(start[0], start[1], 0)


        class Tests(unittest.TestCase):

            def test1(self):
                case = Solution()
                maze = [[0,0,1,0,0],[0,0,0,0,0],[0,0,0,1,0],[1,1,0,1,1],[0,0,0,0,0]] 
                start = [0,4]
                destination = [4,4]
                return self.assertEqual(True, case.canStopAtTarget(maze, start, destination))
            
            def test2(self):
                case = Solution()
                maze = [[0,0,1,0,0],[0,0,0,0,0],[0,0,0,1,0],[1,1,0,1,1],[0,0,0,0,0]]
                start = [0,4]
                destination = [3,2]
                return self.assertEqual(False, case.canStopAtTarget(maze, start, destination))

            def test3(self):
                case = Solution()
                maze = [[0,0,0,0,0],[1,1,0,0,1],[0,0,0,0,0],[0,1,0,0,1],[0,1,0,0,0]]
                start = [4,3]
                destination = [0,1]
                return self.assertEqual(False, case.canStopAtTarget(maze, start, destination))

        if __name__ == '__main__':
            unittest.main()
    ```

- [Number of connected components in an undirected graph](https://www.lintcode.com/problem/591/)

    ```Python
        """
        Number of connected components in an undirected graph
        Given n nodes in a graph, denoted 1 through n. ConnectingGraph3(n) creates n nodes, and at the beginning there are no edges in the graph.

        You need to support the following method:

        connect(a, b), an edge to connect node a and node b
        query(), Returns the number of connected component in the graph
        """

        import unittest



        class connectGraph:

            def __init__(self, n):
                self.parents = [i for i in range(0, n + 1)]
                self.rank = [1 for _ in range(n)]

            def get_parent(self, node):
                p = self.parents[node]
                while p != self.parents[p]:
                    p = self.parents[self.parents[p]]
                return p

            def connect(self, a, b):
                parent_a, parent_b = self.get_parent(a), self.get_parent(b)

                if parent_a == parent_b:
                    return False
                
                if self.rank[parent_a] >= self.rank[parent_b]:
                    self.parents[parent_b] = parent_a
                    self.rank[parent_a] += 1
                else:
                    self.parents[parent_a] = parent_b
                    self.rank[parent_b] += 1

                return True

                
            def query(self):
                nodes = 0
                groups = set()
                for node in self.parents:
                    if node != 0 :
                        p = self.get_parent(node)
                        if p not in groups:
                            nodes += 1
                        groups.add(p)
                return nodes


        class Test(unittest.TestCase):

            def test1(self):
                ans = []
                case = connectGraph(5)
                ans.append(case.query())
                case.connect(1, 2)
                ans.append(case.query())
                case.connect(2, 4)
                ans.append(case.query())
                case.connect(1, 4)
                ans.append(case.query())

                return self.assertEqual(ans, [5,4,3,3])
            
            def test2(self):
                ans = []
                case = connectGraph(6)
                ans.append(case.query())
                ans.append(case.query())
                ans.append(case.query())
                ans.append(case.query())
                ans.append(case.query())
                self.assertEqual(ans, [6,6,6,6,6])

            

        if __name__ == '__main__':
            unittest.main()
    ```

- [1668 Shortest Way to Form String](https://algo.monster/liteproblems/1055)

    ```Python
        def shortestWay(source: str, target: str) -> int:
            count = 0
            target_p = 0  # Pointer for target

            while target_p < len(target):
                # source = 'abc' target = 'abcbc'
                # Start matching with a new subsequence
                count += 1
                source_p = 0  # Pointer for source
                
                # Try to match target[target_p] with source characters
                while source_p < len(source) and target_p < len(target):
                    if source[source_p] == target[target_p]:
                        target_p += 1  # Move to the next character in target
                    source_p += 1  # Move to the next character in source
                    
                # If we can't match anymore, it means we need another subsequence

            return count
    ```

    | Source      | Target      | Expected Output |
    |-------------|-------------|------------------|
    | abc         | ababc       | 2                |
    | abc         | acdbc       | 3                |
    | xyz         | xzyz        | 3                |
    | abc         | cba         | 3                |
    | abcde       | ade         | 1                |
    | abc         | def         | 3                |
    | abacaba     | aaa         | 2                |
    | xyz         | xyzxyz      | 2                |

- [Number of connected components in an undirected graph](Amazon problem)

    ```Python
        """
        Number of connected components in an undirected graph
        Given n nodes in a graph, denoted 1 through n. ConnectingGraph3(n) creates n nodes, and at the beginning there are no edges in the graph.

        You need to support the following method:

        connect(a, b), an edge to connect node a and node b
        query(), Returns the number of connected component in the graph
        """

        import unittest



        class connectGraph:

            def __init__(self, n):
                self.parents = [i for i in range(0, n + 1)]
                self.rank = [1 for _ in range(n)]

            def get_parent(self, node):
                p = self.parents[node]
                while p != self.parents[p]:
                    p = self.parents[self.parents[p]]
                return p

            def connect(self, a, b):
                parent_a, parent_b = self.get_parent(a), self.get_parent(b)

                if parent_a == parent_b:
                    return False
                
                if self.rank[parent_a] >= self.rank[parent_b]:
                    self.parents[parent_b] = parent_a
                    self.rank[parent_a] += 1
                else:
                    self.parents[parent_a] = parent_b
                    self.rank[parent_b] += 1

                return True

                
            def query(self):
                nodes = 0
                groups = set()
                for node in self.parents:
                    if node != 0 :
                        p = self.get_parent(node)
                        if p not in groups:
                            nodes += 1
                        groups.add(p)
                return nodes


        class Test(unittest.TestCase):

            def test1(self):
                ans = []
                case = connectGraph(5)
                ans.append(case.query())
                case.connect(1, 2)
                ans.append(case.query())
                case.connect(2, 4)
                ans.append(case.query())
                case.connect(1, 4)
                ans.append(case.query())

                return self.assertEqual(ans, [5,4,3,3])
            
            def test2(self):
                ans = []
                case = connectGraph(6)
                ans.append(case.query())
                ans.append(case.query())
                ans.append(case.query())
                ans.append(case.query())
                ans.append(case.query())
                self.assertEqual(ans, [6,6,6,6,6])

            

        if __name__ == '__main__':
            unittest.main()
    ```

- [Find the celebrity](https://leetcode.ca/all/277.html)

    ```Python
        # The knows API is already defined for you.
        # @param a, person a
        # @param b, person b
        # @return a boolean, whether a knows b
        # def knows(a, b):

        class Solution(object):
            def findCelebrity(self, n):
                """
                :type n: int
                :rtype: int
                """
                # find the potential celebrity
                candidate = 0
                
                # for each person, check if the potential celebrity knows them
                # if the potential celebrity knows them, then they cannot be the celebrity
                # if the potential celebrity does not know them, then move on to the next person
                for i in range(1, n):
                    if knows(candidate, i):
                        candidate = i
                        # it makes candidate = i since a celebrity MUST be followed by all other nodes.
                        # Check the images of the problem link, in image 1 if node 0 doesn't follow node 1 then candidate will be equal to 2 at the end of this loop. However, it doesn't matter since no celebrity will be found on the next for loop:
                        # The celebrity MUST be inmeditaly reachable on this first loop.
                
                # now we need to validate that the potential celebrity is indeed a celebrity
                # for each person, check if the potential celebrity knows them
                # if the potential celebrity does know them, then they cannot be the celebrity
                # if the potential celebrity does not know them, then check if the person knows the potential celebrity
                # if the person does not know the potential celebrity, then the potential celebrity cannot be a celebrity
                for i in range(n):
                    if i != candidate and (knows(candidate, i) or not knows(i, candidate)):
                        return -1
                return candidate
    ```