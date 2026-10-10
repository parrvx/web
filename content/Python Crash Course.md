## Comments

- A **comment** is a line of text ignored by Python.
- Use a hashtag symbol (`#`) to create a comment.
- The technical name for `#` is octothorpe."

## Data Types

- The real world consists of different types of data (numbers, text, dates, etc).
- A **data type** is a category of data.
- An **integer** is a whole number."
- A **floating-point** is a number with a fractional or decimal component."
- A **string** is a piece of text (a collection of characters in sequence).
- A string can store alphabetic characters, digits, symbols and more.
- The length of a string refers to a count of its characters."
- A **Boolean** is a data type that can only be one of two values: True or False.
- A Boolean represents an evaluation of truth."
- **None** is a value that represents an absent piece of data."

## Operators

- An **operator** is a symbol that performs an operation (mathematical, logical, etc) on one or more values.
- The **operand** is the value or values that the operator is applied to.
- Python includes operators for various mathematical operations: `+` for addition, `-` for subtraction, `*` for multiplication, and `/` for division."
- The `+` operator performs concatenation when applied to strings.
- The `*` operator repeats a string a specified number of times."
- Python follows the PEMDAS rule from mathematics in evaluating operator precedence.
- Precedence refers to which operators will be prioritized in an ambiguous evaluation.

|  | rule |
| --- | --- |
| P | Parentheses |
| E | Exponents |
| M | Multiplication |
| D | Division |
| A | Addition |
| S | Subtraction |

- The division operator performings floating-point division.
- The floor division operator (`//`) leaves off the floating point portion of a division result."
- The modulo operator (`%`) returns the remainder of a division."

## Equality and Inequality Operators

- The equality operator (`==`) compares the equality of two values.
- It returns True if the values are equal and False if they are not."
- The inequality operator (`!=`) compares whether two values are not equal.
- It returns True if two values are unequal and False if they are equal. "
- Python supports mathematical comparison operators (`>`, `>=`, `<`, `<=`).
- The operators return Booleans."

## Variables

- A **variable** is a name for a value in your program. It is a placeholder for the value.
- Multi-word variable names should follow a `snake_case` naming convention."
- The value that a variable represents can *vary* over a program."
- Python evaluates the right-hand side of an equal sign (assignment operator) first."

## Built-in Functions

- A **function** is a reusable procedure. It's a sequence of steps to execute in order.
- A **function** can accept inputs (which are called **arguments**).
- A **function** produces a **return value**, which is the \"output\" of the function.
- The technical term for running/executing a function is \"invoking\" or \"calling\".
- Invoke a function with a pair of parentheses."
- The `len` function returns the length of its argument."
- The `str` function converts its argument to a string."
- The `int` function converts its argument to an integer."
- The `float` function converts its argument to a floating-point.\n"
- The `type` function returns the type of its argument (the kind of value it is)."

## Custom Functions

- Define a function with the `def` keyword, a function name, a parameter list, and a colon.
- Function names should follow a `snake_case` naming convention.
- A **parameter** is a name for an expected input.
- Write the function's logic inside an indented block. The end of the block marks the end of the function logic.
- Variables declared inside a function body will only last as long as the function runs.
- Use the **return** keyword to specify the function's return value (the output).
- When invoking a function, we can pass in arguments sequentially or with explicit parameter names."
- We can assign a default argument to a function parameter.
- Python will supply the default argument if a function invocation does not provide an explicit value."

## String Methods

- An **object** is the technical term for a value in our program. A string is an example of an object.
- A **method** is like a function that belongs to an object.
- To invoke a method, provide a period after the object, then the method name and a pair of parentheses.
- Functions and methods are very similar. Methods are invoked. Methods can accept arguments. Methods can return values.
- Objects can be **mutable** (capable of change) or **immutable** (incapable of change). A string is immutable.
- Common string methods include `upper`, `lower`, `swapcase`, `title`, `capitalize`.\n"

```{python}
profession = "Python Developer"
```

```{python}
profession.upper()
```
```
'PYTHON DEVELOPER'
```

```{python}
profession.lower()
```
```
'python developer'
```

```{python}
profession.swapcase()
```
```
'pYTHON dEVELOPER'
```

```{python}
"once upon a time".title()
```
```
'Once Upon A Time'
```

```{python}
"once upon a time".capitalize()
```
```
'Once upon a time'
```
- The `strip` method removes whitespace from the beginning and end of a string.
- The `lstrip` (left strip) method removes whitespace from the beginning of a string.
- The `rstrip` (right strip) method removes whitespace from the end of a string."

```{python}
profession = "      Python Developer    "
```

```{python}
profession.strip()
```
```
'Python Developer'
```

```{python}
profession.lstrip()
```
```
'Python Developer    '
```

```{python}
profession.rstrip()
```
```
'      Python Developer'
```

- **Method chaining** refers to the invocation of methods on the return values of previous method invocations.
- The code create a link or sequential \"chain\" of methods."

```{python}
profession.lstrip().rstrip().lower()
```
```
'python developer'
```

- The `replace` method swaps all occurrences of a character with another."

```{python}
profession.strip().replace("e", "*")
```
```
'Python D*v*lop*r'
```

- The `startswith` method checks for a substring at the start of a string.

```{python}
profession.strip().startswith("Pyt")
```
```
True
```

```{python}
profession.strip().startswith("pyt")
```
```
False
```

- The `endswith` method checks for a substring at the end of a string."

```{python}
profession.strip().endswith("oper")
```
```
True
```

- The `in` keyword checks for the presence of a substring within a string.
- The `not in` keyword checks for the absence of a substring within a string."

```{python}
"Dev" in profession.strip()
```
```
True
```

```{python}
"Eng" in profession.strip()
```
```
False
```

```{python}
"Eng" not in profession.strip()
```
```
True
```

```{python}
"Dev" not in profession.strip()
```
```
False
```

## Lists

- A **list** is a mutable data structure that holds an ordered collection of values.
- The term **element** describes one value/entry/item in the list."

```{python}
[4, 8, 15, 16, 23, 42]
```
```
[4, 8, 15, 16, 23, 42]
```

```{python}
[True, False, True, True, False]
```
```
[True, False, True, True, False]
```

```{python}
party_attendees = ["Michael", "Freddy", "Jason"]
party_attendees
```
```
['Michael', 'Freddy', 'Jason']
```

- The length of a list is its number of elements."

```{python}
len("Python")
```
```
3
```

```{python}
type(party_attendees)
```
```
list
```

- The `append` method adds an element to the end of the list."

```{python}
presidents = ["Washington", "Jefferson"]
presidents
```
```
['Washington', 'Jefferson']
```

```{python}
presidents.append("Madison")
presidents
```
```
['Washington', 'Jefferson', 'Madison']
```

- The `pop` method removes the last element from the list."

```{python}
popcorn_flavors = ["Salted", "Unsalted", "Caramel"]
popcorn_flavors
```
```
['Salted', 'Unsalted', 'Caramel']
```

```{python}
popcorn_flavors.pop()
```
```
'Caramel'
```

```{python}
popcorn_flavors
```
```
['Salted', 'Unsalted']
```

- The `in` and `not in` keywords check whether or not an element exists within a list."

```{python}
planets = ["Mercury", "Venus", "Earth", "Mars"]
planets
```
```
['Mercury', 'Venus', 'Earth', 'Mars']
```

```{python}
"Earth" in planets
```
```
True
```

```{python}
"Jupyter" in planets
"earth" in planets
```
```
False
```

```{python}
"Pluto" not in planets
```
```
True
```

```{python}
"Mars" not in planets
```
```
False
```

## Tuples

- A **tuple** is a fixed-length, immutable list.
- A tuple cannot be modified after it has been created.
- Technically, the comma symbol declares a tuple.
- The community convention is to wrap a tuple's elements in parentheses.
- Empty tuples require parentheses."

```{python}
foods = "Sushi", "Steak", "Guacamole"
foods
```
```
('Sushi', 'Steak', 'Guacamole')
```

```{python}
foods = ("Sushi", "Steak", "Guacamole")
type(foods)
```
```
tuple
```

## Index Positions and Slices

- Python assigns an index position (an order in line) to every character in a string.
- The index starts counting at 0."

```{python}
hero = "Spiderman"
hero
```
```
'Spiderman'
```

| S | p | i | d | e | r | m | a | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |

- Use square brackets to extract a character/element by index position."

```{python}
hero[0]
```
```
'S'
```

```{python}
hero[1]
```
```
'p'
```

- Use negative values to extract a character/element relative to the end of the object."

| S | p | i | d | e | r | m | a | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| -9 | -8 | -7 | -6 | -5 | -4 | -3 | -2 | -1 |

```{python}
hero[-1]
```
```
'n'
```

```{python}
hero[-5]
```
```
'e'
```

- Use slicing to extract multiple character/elements."

```{python}
hero[1:3]
```
```
'pid'
```

```{python}
hero[:6]
```
```
'Spider'
```

```{python}
hero[7:]
```
```
'man'
```

- Python assigns an index position (an order in line) to every element in a list."

```{python}
superheroes = ["Batman", "Superman", "Wolverine", "Ironman", "Arnold Schwarzenegger"]
```
```
['Batman', 'Superman', 'Wolverine', 'Ironman', 'Arnold Schwarzenegger']
```

```{python}
len(superheroes)
```
```
5
```

```{python}
superheroes = [0]
```
```
'Batman'
```

```{python}
superheroes = [-1]
```
```
'Arnold Schwarzenegger'
```

## Dictionaries

- A **dictionary** is a mutable, unordered collection of key-value pairs.
- A **key** is a unique identifier for a corresponding value.
- The keys must be unique. The values can contain duplicates.
- A dictionary solves the problem of **association** (i.e., mapping two values together).
- Declare a dictionary with a pair of curly braces.
- Write a colon between every key and value.
- Separate each key-value pair with a comma and a space.
- The length of a dictionary is a count of its key-value pairs."

```{python}
menu = {
  "Filet Mignon": 29.99,
  "Bic Mac": 3.99,
  "Pizza": 3.99,
  "Salmon": 3.99
}
menu
```
```
{'Filet Mignon': 29.99, 'Bic Mac': 3.99, 'Pizza': 3.99, 'Salmon': 3.99}
```

The dictionary has $4$ keys and $4$ key-values.

```{python}
len(menu)
```
```
4
```

To extract the key-value.

```{python}
menu["Bic Mac"]
```
```
3.99
```

To add a new key and key-value, or replace a existing key-value of a existing key, it used the operator `=`

```{python}
menu["Burrito"] = 13.99
```
```
3.99
```
To remove a key and key-value, it used the built-in function `pop()`

```{python}
menu.pop("Filet Mignon")
```
```
29.99
```

```{python}
menu
```
```
{'Bic Mac': 3.99, 'Pizza': 3.99, 'Salmon': 3.99, 'Burrito': 13.99}
```

When used the `in` or `not in`, Python consider only the key to evalute it.

```{python}
"Bic Mac" in menu
```
```
True
```

```{python}
5.99 in menu
```
```
False
```

To indicate to Python to consider only the key-values when using the `in` or `not in`, it's used the built-in function `values()`.

```{python}
5.99 in menu.values()
```
```
True
```

## Classes and Objects

- Every value that we've explored so far (5, True, \"Hello\", etc) is an **object**.
- A **class** is a blueprint for creating objects. It is a template, a schematic.
- A **class** defines the methods/functionalities that objects made from it will have.

<img src="./images/Blueprint.avif" alt="image_blueprint" width="200"/>

- We use the class to create one or more objects from the blueprint.
- The object is called an **instance** of the class it is made from.
- The act of creating an object from a class is called **instantiation**.
- Every object we've worked with so far was instantiated from a class.
- In real world terms, a class is the blueprint and the instance/object is the house we build.

<img src="./images/MultipleHouses.jpg" alt="image_blueprint" width="300"/>

- Syntax options like `\"\"` or `[]` or `{}` are shortcuts for instantiation.

```{python}
""
str()
```
```
''
```

```{python}
[]
list()
```
```
[]
```

```{python}
{}
dict()
```
```
{}
```


- For other classes, we'll need to use `class()` syntax to instantiate an object.
- Much like functions and methods, some class constructors will require arguments."

## Importing Modules

- A **module** is a Python file. A file holds various constructs (classes, functions, constants).
- A Python module can import constructs from another module.
- Think of a module like a directory on your computer; it is an organizational container."

### Datetimes

- The Python standard library is a collection of modules built into the language.
- The standard library includes modules for file system interaction, randomness, statistics, etc
- The `import` keyword \"imports\" a module, making it available to use.
- The `datetime` module holds constructs for dealing with dates and times."

```{python}
import datetime
```
### Aliases

- Programmers are notoriously lazy.
- An alias is an alternate name for a value.
- Use the `as` keyword to assign an alias to a module.
- The community convention for the `datetime` module is `dt`."

```{python}
import datetime as dt
```

- The `date` function is a top-level function in the `datetime` module.
- Use `dt.date` to access the `date` class, then parentheses to instantiate it.
- `date` and `datetime `are classes whose names are lowercase (a deviation from the norm).
- The `date` constructor accepts numeric arguments for the year, month, and day."

```{python}
birthday = dt.date(2026,4,12)
birthday
```
```
datetime.date(2026,4,12)
```

As you can see `weekday` has `()` after it, so it it's a method, and you can apply some consideration to it.

```{python}
birthday.weekday()
```
```
6
```

- An attribute is a piece of data belonging to an object.

So, an attribute (like `year`, `month`, `day`), in other hand, doesn't use have `()` after it. And, unlike a method, and you can't apply nothing. Just retrive the information.

```{python}
birthday.weekday()
```
```
6
```

```{python}
birthday.month
```
```
4
```

- To access an attribute value, provide the object, a dot, and the attribute name.
- The `year` attribute represents the year component.
- The complementary `month` and `day` attributes extract the month and day.
- Methods require parentheses, attributes do not."

## Importing Libraries

- A library/package is a bundle of Python code that adds new features to the language.
- The Python ecosystem has packages for web development, database management, chemistry, game engines, etc.
- `polars` is a library for data analysis.
- The `import` keyword imports both modules and packages.
- The community alias for `polars` is `pl`."

```{python}
import polars as pl

pl.Series()
```

### Further Reading

- https://docs.pola.rs/user-guide/installation/#importing"

## Unsigned and Signed Integers"

```{python}
import polars as pl

pl.Series()
```

#### Computer Memory

* Memory is a piece of hardware.
* Memory is a storage location where the computer stores temporary data.
* Programs request memory from the computer (allocation) and the return it back when it is no longer needed (deallocation).
* Memory is finite.

#### How Memory is Measured

* The **bit** is the smallest unit of measurement.
* Think of the **bit** is a box that stores either a $0$ or a $1$.
* $8 bits = 1 byte$
* $1024 bytes = 1 kilobyte$
* $1024 kilobyte = 1 megabyte$
* $1024 megabyte = 1 gigabyte$
* $1024 gigabyte = 1 teragabyte$

#### Python vs Rust

* [Python](https://www.python.org/) has a single `int` type to model whole numbers.
* [Rust](https://rust-lang.org/) has multiple integers types.
* Rust code can use smaller interger types to reduce total memory consumption.

#### Signed vs Usigned Intergers

* Signed intergers support negative and positive values.
* Unsigned intergers support only zero and positive values.
* Unsigned intergers can extend twice as far in the positive direction compared to a signed interger with the same amount of memory.

### A Quick Discussion on Memory

- A bit is the smallest unit of memory in a computer.
- We can think of a bit as a box that stores a 0 or a 1.
- 8 bits is equal to 1 byte. We use different measurement units to account for different scales of data size.

### Integer Types in Rust vs. Python

- Python has a single integer type/class (`int`).
- Polars is built in Rust, and Rust has multiple integer types.
- The integer types fall into two categories: signed and unsigned.
- A signed integer (`Int`) supports both negative and positive values.
- An unsigned integer (`UInt`) supports only zero and positive values."
- The number after `UInt` or `Int` is the number of bits that the integer occupies in memory.
- A `Int16` uses twice the number of bits as an `Int8`.
- The greater the memory, the larger number the type can represent.

| Data type | Lower limit | Upper limit |
| --- | --- | --- |
| Int8 | -128 | 127 |
| Int16 | -32768 | 32767 |
| Int32 | -2147483648 | 2147483647 |
| Int64 | -9223372036854775808 | 9223372036854775807 |

- An unsigned integer can extend twice as far into the positive direction.

| Data type | Upper limit |
| --- | --- |
| UInt8 | 255 |
| UInt16 | 65535 |
| UInt32 | 4294967295 |
| UInt64 | 18446744073709551615 k

```{python}
pl.Int8
pl.Int16
pl.Int32
pl.Int64
```

```{python}
pl.UInt8
pl.UInt16
pl.UInt32
pl.UInt64
```
