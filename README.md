# My Software Engineering Notes

## Python
<details>
  <summary>Expand Python Notes</summary>
  
  ### Decorators
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
  
  A `Generator` in Python is a function that returns an iterator using the `Yield` keyword. In this article, we will discuss how the generator function works in Python.
  
  
  
  ### Yield 
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
  

</details>

## Django
<details>
  <summary>Expand Django Notes</summary>
  
  ### One-to-many Relations
  
  - Use `ForeignKey`
  
  - Related name makes it so that when you want to access an authors book set (by default RELATEDCLASSNAME_SET [book_set]) you use the provided related name 'books' instead of the default 'book_set'.
  
  ```class Books
      author = models.ForeignKey(Author, on_delete=models.CASCADE, null=True, related_name='books') # Can be null if no value is provided
  ```
  
  ### Many-to-many Relations
      
  - Use `ManyToManyField`
  
  ```
  # In this case, related_name is used to get all the books of a country by using 'books' (in this case) instead of 'book_set'
  class Book
      published_countries = models.ManyToManyField(Country, related_name='books')
  ```
  
  ### One-to-One Relations    
      
  - Use `OneToOneField`
  
  - Related name is not needed here since Django automatically will link authors to the Address object it belongs to. This means you can access an author object from its adress like 'Address.objects.all()[0].author'
  
  ```
  class Author
      address = models.OneToOneField(Address, on_delete=models.CASCADE, null=True)
  ```
</details>
