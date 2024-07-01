### Decorators

---

Python decorators are a powerful feature that allows you to modify or extend the behavior of functions or methods without changing their actual code. They essentially allow you to wrap another function or method and execute code before and/or after the wrapped function runs. Decorators are typically denoted by the @ symbol followed by the decorator function name, placed just above the function definition.

Here's a basic example to illustrate how decorators work:

``` Python
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

In this example, my_decorator is a decorator function that takes another function func as its argument. Inside my_decorator, a nested function wrapper is defined, which wraps around the original function func. Inside wrapper, you can include code to be executed before and/or after calling func. Finally, the wrapper function is returned.

When you decorate the say_hello function with @my_decorator, Python essentially does this: say_hello = my_decorator(say_hello). So, when you call say_hello(), it actually calls the wrapper function created by my_decorator, which in turn calls the original say_hello function within it.

Some of the most common decorators used in Python include:

``` Python
@property # Used to define properties on classes, allowing you to define getter, setter, and deleter methods for attributes.

@classmethod # Declares a method within a class that takes the class itself as its first argument instead of the instance.

@staticmethod # Used to declare a method that belongs to the class but doesn't require access to the class or instance.

@abstractmethod # Used in abstract base classes to declare abstract methods, which must be implemented by subclasses.

@wraps # A decorator from the functools module used to preserve the metadata of the original function when creating wrapper functions. This is particularly useful for maintaining docstrings, function name, and other attributes.

@lru_cache # A decorator from the functools module that caches the results of a function, saving time when the same inputs occur again.
```

### Dunder Methods 

---

Dunder methods, short for "double underscore" methods, are special methods in Python that have names surrounded by double underscores, like `__init__`, `__repr__`, `__add__`, etc. They are also called magic methods or special methods.

These methods allow classes to define specific behavior that gets invoked in response to certain operations or interactions. For example, when you use the + operator with instances of a class, Python looks for the __add__ method to determine how to perform addition for those objects.

Here are some common dunder methods and their purposes:
``` Python
__init__(self, ...) # Constructor method that initializes a new instance of a class.
__repr__(self) # Method that returns a string representation of the object, used for debugging and logging.
__str__(self) # Method that returns a string representation of the object, used for informal representation to end-users.
__len__(self)# Method that returns the length of the object.
__getitem__(self, key) # Method that enables accessing elements of an object using square brackets, like obj[key].
```

### Iterators

---

An iterator in Python is an object that is used to iterate over iterable objects like lists, tuples, dicts, and sets. The Python iterators object is initialized using the `iter()` method. It uses the `next()` method for iteration.
``` Python
__iter__() # The iter() method is called for the initialization of an iterator. This returns an iterator object
__next__() # The next method returns the next value for the iterable. When we use a for loop to traverse any iterable object, internally it uses the iter() method to get an iterator object, which further uses the next() method to iterate over. This method raises a StopIteration to signal the end of the iteration.
```

``` Python
string = "GFG"
ch_iterator = iter(string)
 
print(next(ch_iterator)) # -> G
print(next(ch_iterator)) # -> F
print(next(ch_iterator)) # -> G
```

### Generators

---

A `Generator` in Python is a function that returns an iterator using the `Yield` keyword. In this article, we will discuss how the generator function works in Python.



### Yield 

---

`Generators` are a special type of iterable that allow you to iterate over a sequence of values lazily, meaning that they produce values on-the-fly as they are requested rather than generating the entire sequence upfront and storing it in memory.

When you use `yield` inside a function, it turns that function into a generator function. Instead of using return to return a single value and exit the function, yield is used to yield a value to the caller while suspending the state of the function. This allows the function to be resumed from where it left off the next time it is called.

Here's a simple example:
``` Python
def count_up_to(n):
    count = 1
    while count <= n:
        yield count
        count += 1

# Using the generator function
counter = count_up_to(5)
print(next(counter))  # Output: 1
print(next(counter))  # Output: 2
print(next(counter))  # Output: 3
```

In this example, count_up_to is a generator function that yields numbers from 1 up to n. When you call next(counter), it starts or resumes execution of the generator function until the next yield statement, where it yields the value and pauses execution. The function retains its state, so subsequent calls to next() continue from where it left off.

Using yield allows for memory-efficient iteration over large sequences, as only one value needs to be stored in memory at a time, unlike with lists where the entire sequence is stored. Additionally, it enables lazy evaluation, meaning that values are generated only when needed, which can improve performance in certain scenarios.

### Zip

---

The zip() function in Python is used to combine multiple iterables (lists, tuples, etc.) element-wise. It takes in two or more iterables as arguments and returns an iterator that generates tuples of corresponding elements from each iterable.

Here's a basic example:

```python
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']

zipped = zip(list1, list2)

for item in zipped:
    print(item)
# Output:

(1, 'a')
(2, 'b')
(3, 'c')
```

In this example, zip() pairs the first element of list1 with the first element of list2, the second element of list1 with the second element of list2, and so on.

One important thing to note about zip() is that it stops generating tuples as soon as one of the input iterables is exhausted. For example:

```python
list1 = [1, 2, 3]
list2 = ['a', 'b']

zipped = zip(list1, list2)

for item in zipped:
    print(item)
# Output:

(1, 'a')
(2, 'b')
```

Here, since list2 has only two elements, the third element of list1 is ignored.

If you want to get a list of tuples instead of an iterator, you can use the list() function to convert the iterator returned by zip() into a list:

```python
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']

zipped = list(zip(list1, list2))

print(zipped)
# Output:

[(1, 'a'), (2, 'b'), (3, 'c')]
```

zip() is commonly used in scenarios where you need to iterate over multiple lists simultaneously, especially when the lists are related and you want to process their elements together.

### Serialization

---

Serialization in Python refers to the process of converting complex data structures, such as objects or data collections, into a format that can be easily stored or transmitted and later reconstructed back into its original form. This process is essential for tasks like saving data to a file, sending data over a network, or storing data in a database.

Python provides several built-in modules for serialization, such as:

- pickle: This module can serialize Python objects into a binary format. It can handle almost any Python object, including custom classes and functions.

- json: This module serializes Python objects into a human-readable format called JSON (JavaScript Object Notation). JSON is commonly used for transmitting data between a server and a client over a network.

- marshal: This module is similar to pickle but is more restricted in terms of the types of objects it can serialize. It is primarily used for serializing Python code objects.

- shelve: This module provides a simple interface for persistently storing Python objects in a dictionary-like format.

Serialization is particularly useful for tasks like data storage, data exchange between different systems or languages, and caching. However, it's essential to consider security implications, especially when deserializing data, as it can lead to security vulnerabilities if not handled properly.

### Lambda Functions

---

Lambda functions in Python are small, anonymous functions defined using the lambda keyword. They are often used when you need a short function for a short period of time and don't want to define a full function using def.

#### Syntax
The syntax of a lambda function is:

```Python
lambda arguments: expression
```
- lambda is the keyword used to define a lambda function.
- arguments are the input parameters for the function.
- expression is a single expression that gets evaluated and returned as the result of the function.
#### Examples

##### Basic Example:

```Python
square = lambda x: x ** 2
print(square(5))  # Output: 25
```

Here, lambda x: x ** 2 defines a lambda function that takes one argument x and returns its square.

##### Using Multiple Arguments

```Python
add = lambda x, y: x + y
print(add(3, 4))  # Output: 7
```

This lambda function lambda x, y: x + y takes two arguments x and y and returns their sum.

##### In List Sorting
Lambda functions are often used in conjunction with built-in functions like sorted() or filter():

```Python
points = [(1, 2), (3, 1), (5, 4), (2, 7)]
points_sorted = sorted(points, key=lambda x: x[1])
print(points_sorted)  # Output: [(3, 1), (1, 2), (5, 4), (2, 7)]
```

Here, lambda x: x[1] specifies that the list should be sorted based on the second element of each tuple in points.

##### As an Argument to map()

```Python
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # Output: [1, 4, 9, 16, 25]
```

The lambda function lambda x: x ** 2 is applied to each element in numbers using map() to compute their squares.

#### Benefits of Lambda Functions
- Conciseness: They reduce the amount of code when a simple function is needed.
- Readability: Lambda functions can make code more readable when used appropriately, such as within map(), filter(), or sorted().
#### Limitations
- Single Expression: Lambda functions are restricted to a single expression, making them unsuitable for complex logic.
- No Statements: They cannot contain statements like return, pass, or assert.

Lambda functions are particularly useful in functional programming contexts where functions are treated as first-class citizens and are passed around as arguments or returned from other functions