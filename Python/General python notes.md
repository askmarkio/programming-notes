Links: [Projects](Projects)
# Problem areas

## functions

In Python, when you define a function, you don't always have to explicitly specify what to return. If you don't use a return statement, Python implicitly returns `None` by default.

For example, in your original `curse()` function, you have a `return` statement without any value:

```python
def curse(weapon_damage):
    lesser_cursed = (weapon_damage * .5) - weapon_damage
    greater_cursed = (weapon_damage * .5) - weapon_damage
    return
```

Here, if you call `curse()`, it will return `None` because no value is explicitly returned.

However, if you want your function to calculate something and return the result, you need to use a return statement to specify what value or values to return.

So, to answer your question, you don't always have to specify what to return, but if you want your function to produce a meaningful result, you typically should. Otherwise, the function might not behave as expected when called in other parts of your code.
via ChatGPT

**Best practice**
Specify your return type. It makes it easier to read as well as benefits others who may read your code.
```python
def get_users() -> dict[int,str]:
	users: dict[int,str] = {1: 'Bob', 2: 'April', 3: 'Ty'}
	return users
```
In the above we specify the type of data that it takes. Can be helpful if we accidentally pass a type that isn't allowed.
### placeholders
In Python, placeholders are used to reserve a spot for data that will be inserted into a string, format, or template at a later point. Placeholders are typically used in string formatting to dynamically insert values into a string.

There are different ways to create and use placeholders in Python, including:
1. Using the `%` operator for string formatting:
```python
name = "Alice"
age = 30
formatted_string = "My name is %s and I am %d years old." % (name, age)
print(formatted_string)
```

2. Using the `str.format()` method:
```python
name = "Bob"
age = 25
formatted_string = "My name is {} and I am {} years old.".format(name, age)
print(formatted_string)
```

3. Using f-strings (formatted string literals) in Python 3.6 and above:
```python
name = "Charlie"
age = 35
formatted_string = f"My name is {name} and I am {age} years old."
print(formatted_string)
```

In each of these examples, `{}` or `%s`, `%d` are placeholders where the values of `name` and `age` are inserted. Placeholders provide a flexible way to create dynamic strings with variable content.

**Best Practice** 
Do not use `pass` or `...` as a placeholder. Instead use the following: 
```python
raise NotImplementedError()
```
The other two place holders will not error if you forget to return to the code to finish its implementation. Using the above will allow it to error out when being run. Further, you can add text to explain why you did not do it:
```python
raise NotImplementedError("I was too lazy to finish this.")
```

## f-strings

If you want to set a variable with text that includes references to other variables, you can use string formatting or f-strings in Python. Here's how you can do it:

Using String Formatting:
```python
name = "Alice"
age = 30
message = "Hello, my name is {} and I am {} years old.".format(name, age)
print(message)
```

Using f-strings (available in Python 3.6 and later):
```python
name = "Alice"
age = 30
message = f"Hello, my name is {name} and I am {age} years old."
print(message)
```

Both methods achieve the same result: they interpolate the values of `name` and `age` into the string `message`. Choose whichever method you find more readable or convenient.
-via ChatGPT


## If statements

```python
if condition1:
    # Block of code to execute if condition1 is True
elif condition2:
    # Block of code to execute if condition2 is True
elif condition3:
    # Block of code to execute if condition3 is True
...
else:
    # Block of code to execute if none of the above conditions are True
```


### Comparisons
Obviously you can do comparisons with if statements like `if 2 < 3`
#### not
Not to be confused with None, Not is a logical operator that returns a `True` or `False`. This is logical negation. It returns `True` if the operand is `False` and vice-versa. You can use it when you want to represent the absence of a value.
```python
# Using None
value = None

if value is None:
    print("The value is not assigned yet")
else:
    print("The value is:", value)

# Using not
is_empty = True

if not is_empty:
    print("The container is not empty")
else:
    print("The container is empty")
```

Use None to show the absence of a value or null value i.e., use when a variable has not been set.

*Wrong usage*
```python
def get_first_item(items):
    if items is None:
        return "ERROR"
    else:
        return items[0]
```

The above will produce an out of bound exception error because I am checking if `items` variable has been set (in my work example, this is a list). But since it was actually set it will error out. Since I want to check if the list `items` is empty, I should use `not`
*Good usage*
```python
def get_first_item(items):
    if not items:
        return "ERROR"
    else:
        return items[0]
```

*Alternative solution*
```python
def get_first_item(items):
    if len(items) == 0:
        return "ERROR"
    return items[0]
```

I forgot that length checks existed for this issue, but I can check the length of the list to see if it is empty.
## Loops

For 
```python
for variable in sequence:
    # Do something with variable
```
Example
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

Range
You can use the range() function if you want to repeat an action a specific number of times:
```python
for i in range(5):  # Will iterate from 0 to 4
    print(i)
```
Example
```python
colors = ["red", "green", "blue"]
fruits = ["apple", "banana", "cherry"]

for color in colors:
    for fruit in fruits:
        print(f"{color} {fruit}")
```

Iteration is also done with ranges using the same formula. Here is an example of iterating through a list:
```python
for i in range(0, len(sports)):
    print(sports[i])
```
What this means is that for whatever the number is (i) in the range of 0 to whatever the length of the list sports is, print each item (i) in the sports list.
It's important to note that an array list have values starting at 0 for the first entry.

No-index / no-range syntax
If you only need to get the values of what is in the array, you can forego using the index numbers and just specify the type. For example,
```python
trees = ['oak', 'pine', 'maple']
for tree in trees:
    print(tree)
# Prints:
# oak
# pine
# maple
```

Instead of doing a `for i` to indicate the index, we simply replace it with the type. This can make the code cleaner.

Example: Max number

```python
def find_max(nums):
    max_so_far = float("-inf")
    for num in nums:
        if num > max_so_far:
            max_so_far = num
    return max_so_far
```

We find the max number in a list and set the `max_so_far` to be that value. While dealing with numbers, we will get a compile error if we deal with is as a range:

`for i in range(0, nums):`

The following error is produced:
```
TypeError: 'list' object cannot be interpreted as an integer
```

I think the problem, even after setting it to `len(nums)`, is that `nums` is obviously not an integer. Using `len` converts it to an integer because it now returns the length of the list—an integer.  But we don't need this to find the max number. 

In the max sum problem, we just want to compare each item. We start with a negative infinity value, so anything will be larger than it. Each iteration sets the value and compares the next in the list to the new value. Once the list is complete, what remains is the largest value.
#### Loop Control Statements:

- `break`: Exits the loop.
- `continue`: Skips the rest of the code inside the loop for the current iteration and moves to the next iteration.
- `pass`: Does nothing; used as a placeholder.

## Operators
```python
remainder = 8 % 3
# remainder = 2

remainder = 9 % 3
# remainder = 0
```

This is called modulo operator that returns the remainder of the division of the left operand by the right. 

The general view is that if it ends in 0 it is an even number and an odd if it has a remainder.
## Lists
All about lists

### Append
Say you have a list `cats[]` and you want to add a new value to it. You would do so like this:

```python
cats.append("bengal")
```

In the above, we add bengal cat to the list of cats.

### Remove/Pop
To remove from a list and store its value, you use `pop`:

```python
animal = cats.pop()
# animal will return bengal
```

Written as so, pop will remove the last element from a list and return it to us.

### Step/Slicing
In Python, when working with lists, you can use the step parameter in slicing to specify the increment between elements to be selected. The step parameter allows you to select elements at regular intervals from a list. 

Here is an example to demonstrate how to use the step parameter in list slicing:

```python
# Define a list
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# Select elements with a step of 2
selected_numbers = numbers[::2]

# Print the selected elements
print(selected_numbers)  # Output: [0, 2, 4, 6, 8]
```

In this example, `numbers[::2]` selects elements from the `numbers` list with a step of 2, which means every second element is selected. The resulting list `selected_numbers` contains elements `[0, 2, 4, 6, 8]`.

Another example

```python
scores = [50, 70, 30, 20, 90, 10, 50]
# Display list
print(scores[1:5:2])
# Prints [70, 20]
```

I was confused because in the 1st index spot is 70 and in the 5th is 10, so why was it printing the 3rd index spot, which was 20?

As we slice the list above, remember that the start of the slice is **inclusive** and the stop of the slice is **exclusive**. So the value 10 was outside of the scope because it was in the 5th index and that was exclusive.

### Contains
You can check to see if a value exists in a list like so:
```python
fruits = ["apple", "orange", "banana"]
print("banana" in fruits)
# Prints: True
```

### Deletes
You can delete items from lists or an entire slice. Unlike pop, it will not store what you deleted
```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]

# delete the fourth item
del nums[3]
print(nums)
# Output: [1, 2, 3, 5, 6, 7, 8, 9]

# delete the second item up to (but not including) the fourth item
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
del nums[1:3]
print(nums)
# Output: [1, 4, 5, 6, 7, 8, 9]

# delete all elements
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
del nums[:]
print(nums)
# Output: []
```

### Reverse
You can reverse a list by using step
```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
reverse_nums = nums[::-1]
print(reverse_nums)
```

In the above, we create a new list and [[#Step/Slicing]] through it backwards with `-1` which will start at the end of the list.
In the class example, the solution was as follows: 
```python
def reverse_array(items):
    new_array = []
    for i in range(len(items) - 1, -1, -1):
        new_array.append(items[i])
    return new_array
```
Although, I don't understand the addition -1 values. I can see it is gettin the length of the list and subtracting one, but what are the other for?
Apparently, the above is the Start, Stop, Step format. The length of the list - 1 is the Starting position, which would make it the end of the list. The next is the Stop, telling it to stop before the -1 index. Then the last is telling it to Step in reverse by 1.
- [x] Find out what the other two above mean

### Split
```python
message = "This is a message"
words = message.split()
# Will return "this, is, a, message"
```

This method is used on strings to split them up individually to words.

### Join
```python
my_list = ['Hello', 'World', 'Python']
result = ' '.join(my_list)
print(result)
# This will return "Hellow World Python"
```

This method is used on strings to split them up individually to words. In the above, we are using white space as the join identifier. For example, you can use `', '` to join at the comma.

## Tuples
These are like lists but have a fixed size, are ordered, and unchangeable. They are created with round brackets.

```python
my_tuple = ("this is a tuple", 45, True)
print(my_tuple[0])
# this is a tuple
print(my_tuple[1])
# 45
print(my_tuple[2])
# True
```

Can have multiple lists and retrieve from either one
```python
my_tuples = [("this is the first tuple in the list", 45, True),("this is the second tuple in the list", 21, False)]
print(my_tuples[0][0]) # this is the first tuple in the list
print(my_tuples[0][1]) # 45
print(my_tuples[1][0]) # this is the second tuple in the list
print(my_tuples[1][2]) # False
```


## Errors and exceptions



## Sets
set()


## Classes

I have zero idea about why I am having a bad time with these. Here is a recent problem that I wrote to resolve:

url: https://www.boot.dev/lessons/d0da006c-6562-41c0-a7f6-93e795cf078d

The question
"""

Library

You've been tasked with writing some code for your public library, complete the Library and Book classes listed below.
Book class
__init__(self, title, author)

Set .title and .author to the values of the parameters.
Library class

Add the following methods.
__init__(self, name)

Initialize a .name member variable to the value of the name parameter. Create a .books member initialized to an empty list.
add_book(self, book)

Add book, a Book instance, to the books instance variable by appending it to the end of the list.
remove_book(self, book)

If the book's title and author match a library book's title and author, the remove_book method should remove that library book from the list.
search_books(self, search_string)

For every book in the library check if the search_string is contained in the title or author field (case insensitive). Return a list of all books that match the search string, ordered in the same order as they were added to the library.
Hints

You can use the .lower() method to convert a string to lowercase.
"""


Here was the solution I painstakenly came up with after lots of hints and suggestions:


"""
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author


class Library:
    def __init__(self, name):
        self.name = name
        self.books = []

    def add_book(self, book):
        self.books.append(book)

    def remove_book(self, book):
        for libbook in self.books:
            if libbook.title == book.title and libbook.author == book.author:
                self.books.remove(libbook)

    def search_books(self, search_string):
        results = []
        for book in self.books:
            if search_string.lower() in book.title.lower() or search_string.lower() in book.author.lower():
                results.append(book)
        return results 
"""


Now I will walk myself through the code to help in my understanding. I'll return to this later and correct if I am wrong.

I keep having issues creating instances of the class when it isn't needed. Here is an early copy of the code:
"""
def add_book(self, book):
    book = Book(title, author)  # This line recreates the book
    self.books.append(book)
"""
This is an example of me not reading what the existing method is doing. I was instantiating a new book object and overwritting the book that was being supplied in the method.

In the classes, we are using an constructor which gives the defaults for an object, which can be overwritten inside a module.
These default variables are accessible to all modules to call.





## Documentation
Ways to add documentation to your code. These are called docstrings. It must be the first line after a method, class, function.

```python
def get_users() -> dict[int,str]:
"""
Retrieves the ids and usernames from a database as a dict.

:return: dict[int, str]
"""

	users: dict[int,str] = {1: 'Bob', 2: 'April', 3: 'Ty'}
	return users
```
source: https://peps.python.org/pep-0257/

If you were to hover over the function call (get_users but it's not being called in this example), the documentation will display. 

