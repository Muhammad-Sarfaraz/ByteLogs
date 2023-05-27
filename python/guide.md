# Python

Total Data Types
1. Numeric Types:
   - int
   - float
   - complex

2. Sequence Types:
   - str
   - bytes
   - bytearray
   - list
   - tuple
   - range

3. Mapping Type:
   - dict

4. Set Types:
   - set
   - frozenset

5. Boolean Type:
   - bool

6. None Type:
   - None

7. Date and Time Types (modules):
   - datetime
   - time
   - calendar

8. Mathematical Functions (module):
   - math

9. Decimal Type (module):
   - decimal

10. Fraction Type (module):
    - fractions

11. Regular Expressions (module):
    - re

12. File and Directory Access (modules):
    - os
    - os.path
    - glob

13. Command Line Arguments (module):
    - sys

14. Console Input and Output (module):
    - input
    - print

15. Type Functions and Type Checking:
    - type
    - isinstance

16. Iterator Types (module):
    - iter
    - next

17. Enumerations (module):
    - enum

18. Data Compression and Archiving (modules):
    - zlib
    - gzip
    - zipfile

19. Cryptographic Services (module):
    - hashlib

20. JSON Encoding and Decoding (module):
    - json


* Variables and Data Types:

```
# Integer variable
age = 25

# Float variable
temperature = 98.6

# String variable
name = "John Doe"

# Boolean variable
is_active = True

# List variable
fruits = ["apple", "banana", "orange"]

# Tuple variable
point = (3, 4)

# Dictionary variable
person = {"name": "Alice", "age": 30}

```

* Control flow
```
# if-elif-else statement
x = 10
if x > 0:
    print("Positive")
elif x < 0:
    print("Negative")
else:
    print("Zero")

# for loop
fruits = ["apple", "banana", "orange"]
for fruit in fruits:
    print(fruit)

# while loop
count = 0
while count < 5:
    print(count)
    count += 1

# break and continue
for i in range(10):
    if i == 3:
        break
    if i == 1:
        continue
    print(i)

```

#### Function:

```
# Function with parameters and return value
def add_numbers(a, b):
    return a + b

result = add_numbers(3, 5)
print(result)  # Output: 8

# Function with default parameter value
def greet(name="Guest"):
    print("Hello, " + name)

greet()          # Output: Hello, Guest
greet("Alice")   # Output: Hello, Alice

# Function with docstring
def square(number):
    """
    Returns the square of a number.
    """
    return number ** 2

print(square(4))  # Output: 16
print(square.__doc__)  # Output: Returns the square of a number.

```

#### Modules and Packages:

```
import math

radius = 5
area = math.pi * math.pow(radius, 2)
print(area)  # Output: 78.53981633974483
```

* File I/O:

```
file_path = "my_file.txt"

with open(file_path, "r") as file:
    content = file.read()
    print(content)
```

#### Object-Oriented Programming (OOP):
```
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

# Creating objects
rectangle1 = Rectangle(5, 3)
rectangle2 = Rectangle(4, 6)

# Accessing object properties and methods
print(rectangle1.length)    # Output: 5
print(rectangle2.area())    # Output: 24
```

#### Type casting

Int:
```
num_str = "123"
num_int = int(num_str)
```

Float:
```
num_str = "3.14"
num_float = float(num_str)
```

String:
```
num_int = 123
num_str = str(num_int)
```

### Tupeles:
- Tuples are typically used to store a collection of related values as a single entity.
- Tuples are ordered and immutable sequences of elements.

```
person = ("John", 25, "New York")
```

#### Dictionaries:
- Dictionaries are unordered collections of key-value pairs.
- Dictionaries are enclosed in curly braces { } or can be created using the dict() constructor.
- Dictionaries provide efficient look-up based on keys.

```
person = {"name": "John", "age": 25, "city": "New York"}
```

#### Sets

- Sets are unordered collections of unique elements.
- Sets are enclosed in curly braces { } or can be created using the set() constructor.
- Sets automatically remove duplicate elements, and they do not preserve the order of insertion.
- Sets provide operations like union, intersection, difference, and more.

```
fruits = {"apple", "banana", "orange"}
```