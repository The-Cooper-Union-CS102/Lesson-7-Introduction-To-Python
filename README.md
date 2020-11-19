# Introduction to Python

## When to Use Python

Python is an *interpreted* language, meaning you do not have to compile your
program.  It is very easy to read and write Python code compared to most other
languages.  However this ease comes at some costs.  It does not have type safety,
and it is generally slow.

These downsides are often reduced by the fact that you can write performance or
safety critical code in other languages, and then use that code in Python.  One
place Python shines is it's *ecosystem* of support from open source communities.
For example, most machine learning and data science libraries target Python as
their main developer interface.

In short, you should use Python if you just need to get something done quickly,
as a prototype for a faster language, or if you need code that exists in the
Python ecosystem.

## Interpreted Languages

The first major difference between Python and C which makes it easier to use is
the fact that it is interpreted.  This convenience comes at the cost of speed.
Other interpreted languages you might need to learn in the future include
MATLAB and JavaScript.

## Type Safety

Python is about the least type safe as you can get.  There is absolutely no
type checking.  One moment a variable can an integer and, the next it can be a
float, and next it is a string.  There is no limit as to what a single variable
can represent.  There is some static type checking available through the *mypy*
library, however it is rarely used.

## Demonstration

You can bring up the Python *interpreter* by running `python` in bash, if you
have it installed.  Now let's see what we can do.

## Output

First, you can print to the screen with `print` (rather than `printf` as in C).
Below is a simple *hello world* program written in Python.

```python
print('Hello, world')
```
```
Hello, world
```

## Basic Types

The built in Python types are fairly similar to the built in C types, but we do
get some more functionality as well.  Let's take a look.

### `int`

Integers are mostly the same in Python, with one beautiful exception: they never
oerflow!  For example, take a look at the result of this operation which would
certainly overflow on any built in C integer:

```python
print(99999999999999**99)
```
```
999999999999010000000000485099999999843151000000037643759999992847685600001120529255999851129684560017120086275598268969054356155792785107947394947386720524370524973834138280251750760077070249614262299352520961229283992691098805546237395498858449258839259192423512729632303161582885260972810897704383804273946418451779695030082461359353097523360920141070562702780630312564401226649149811282071692215918962327203736770314652100657366063652070169315601433509462464798923249120353677790956846435567057863700541236449924465090719080970157876897926927682137631629508275121669937275752256199910415892799682414285193258908697965193904268511742261304374373830694332631557059746356077893164791881199330009837311377700126063441924089765303940088294707422260075862517364457132402907102774904262625670503551849986724698785516808417616137889446203230753156540587562996837654939896050004692482809720434647211051496417785329401426740564518619624990501103555681289381672426740244832832474557304733501089853069369718250203785892821951883509025223446345369915911208705358160313111022956144424057114739080091357036769533255907408076168514501141549724390119445378661887707160067784737700647489963992292975017658617197482529475629475026105260505261328038442072148920401731030945643998287991372440001488703154399998879470744000000715231439999999623562400000000156848999999999951490000000000009899999999999999
```

By the way, the `**` in that example is exponentiation.

### `float`

Floats again, are very similar to their C counterparts.  The exception is that
really there is no such thing as a 32-bit float in Python.  Everything is a
64-bit double.  That means they are still susceptible to underflow and overflow
just as they were in C.

```python
print(1 / 2)
print(1e-456)
print(1e456)
```
```
0.5
0.0
inf
```

Note that the above code will run differently depending on whether you are
running Python 2 or 3.  In Python 2 (now deprecated) the first print statement
will print 0, as it would in C.  However in Python 3 the division of two
integers yields a float by default.

### `str`

Unlike C, there is no `char` type in Python.  Everything is a string, so if you
want a single character, that is just a string of length 1.  Unlike C strings,
you usually do not have to deal with the dirty details of the string like the
null terminator, and there are several built in methods that can help you.
Also, unlike C strings, Python strings are **immutable**.  This means once
you create a string, you cannot change it.

```python
string = 'Hello, world!'
print(string.endswith('world!'))
print(',' in string)
print(string[0:5])
print(string[-1])
print(string.split())
```
```
True
True
Hello
!
['Hello,', 'world!']
```

Formatting strings is way easier in Python.  Here are some different
ways you can format a string

```python
age = 23
greeting = 'hi'
gpa = 3.0

str1 = greeting + ' I am ' + str(age) + ' years old and my gpa is ' + str(gpa)
print(str1)

str2 = '%s I am %s years old and my gpa is %s' % (greeting, age, gpa)
print(str2)

str3 = '{} I am {} years old and my gpa is {}'.format(greeting, age, gpa)
print(str3)

str4 = '{greeting} I am {age} years old and my gpa is {gpa}'.format(
        greeting=greeting, age=age, gpa=gpa)
print(str4)

str5 = f'{greeting} I am {age} years old and my gpa is {gpa}'
print(str5)
```
```
hi I am 23 years old and my gpa is 3.0
hi I am 23 years old and my gpa is 3.0
hi I am 23 years old and my gpa is 3.0
hi I am 23 years old and my gpa is 3.0
hi I am 23 years old and my gpa is 3.0
```

### Tuple

A tuple is similar to an array in C, with they key exception that it is
**immutable** (again meaning it can not be modified once created) and that
it can store any number of different types.

```python
a = (1, '2', 3.0)
print(a)
print(a[1])
```
```
(1, '2', 3.0)
2
```

Note in the above case, the parentheses are not necessary,
the same program would work fine removing them.

```python
a = (1, 2, 3)
a[1] = 3
```
```
Traceback (most recent call last):
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/tuplebad.py", line 2, in <module>
    a[1] = 3
TypeError: 'tuple' object does not support item assignment
```

One nice Python feature is tuple assignment.  If you have a
tuple containing N elements, you can easily assign the
values to N variables like so:

```python
a, b, c = (1, 2, 3)
print(a)
print(b)
print(c)
```
```
1
2
3
```

This applies with any tuple stored in variables as well,
for example:

```python
z = 1, 2, 3
a, b, c = z
print(a)
print(b)
print(c)
```
```
1
2
3
```

### None

The `None` type is very simple.  It does not hold any value
and you actually can't have a `None` object.  It is just the
type itself.  It is most similar to the `NULL` pointer in C.
You can use it to represent an empty or invalid result.
Usually one does not perform an operation on it, you just
check if something is `None`.  We will see some examples
later on.

### Pointers and Arrays

There are no pointers in Python!  That's right, the hardest part of C is just
not here.  They are working under the hood but they are virtually never exposed
in pure Python code.  That means with the above types, you can never have the
same kind of behavior you had in C of passing a pointer and modifying it.  We
can still emulate this behavior, but we will need either a class or one of the
following advanced types.

Arrays are technically present in Python, but they are so rarely used that we
will forego any explanation.

## Advanced Types

The types above will give you almost everything you had in C (except pointers)
but now we will go through some "advanced types" which give us even more power.
These are not actually advanced because they are very commonly used in Python,
they just have no C alternative

### List

Lists are the typical replacement of arrays in C, but they are much more
powerful.  Here is a simple example.

```python
a = [] # Create an empty list
print(a)
a.append(3.14)
print(a)
a.append(1)
print(a)
a.sort()
print(a)
b = a * 2
print(b)
z = [1] * 10 # Create a list of 10 ones
print(z)
r = list(range(10)) # Create a list of 0-9
print(r)
print(sum(r))
print(sum(r)/len(r)) # Get the average
r.reverse()
print(r)
print(max(r))
print(min(r))
```
```
[]
[3.14]
[3.14, 1]
[1, 3.14]
[1, 3.14, 1, 3.14]
[1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
45
4.5
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
9
0
```

### Set

A set is a data structure that allows very quick look up for elements.  It has
similar semantics as a list, except it is unordered and faster in most cases.

```python
a = set(range(100)) # create a set of numbers 1-100
print(a)
print(50 in a)
print(200 in a)
a.remove(50)
a.add(200)
print(50 in a)
print(200 in a)
x = set(range(75)) # Create a set of numbers from 0 to 74
y = set(range(50, 100)) # Create a set of numbers from 50 to 100
print(x.intersection(y)) # Get the numbers that are in boths sets
print(x.union(y)) # Get the numbers that are in either set
```
```
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99}
True
False
False
True
{50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74}
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99}
```

Here is a speed comparison between a set and a list for looking up a number.

```
python3 -m timeit --setup 'a = set(range(100000))' '50000 in a'
5000000 loops, best of 5: 48.6 nsec per loop
```

```
python3 -m timeit --setup 'a = list(range(100000))' '50000 in a'
500 loops, best of 5: 727 usec per loop
```

As you can see, for a large list of integers, the set lookup (48.6 nanoseconds)
is much much faster than a list lookup (727 microseconds) by a factor of 15000!

Here we used the example of integers, but sets work with almost any **basic**
data type, and they are especially useful with strings.  Note that they do
not work with advanced data types like lists, sets, and dictionaries.

```python
a = set() # create an empty set
# These examples all give errors
a.add(list())
s.add(dict())
s.add(set())
```
```
Traceback (most recent call last):
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/setbad.py", line 3, in <module>
    a.add(list())
TypeError: unhashable type: 'list'
```

Sets have no alternative in C, except if you code the data structure itself.
If you want to learn how a set works under the hood, take the data structures
and algorithms class.

### Dictionary (Hash Table)

A dictionary (which is really the more well-known "hash table") is very similar
to a set, except that a value is also stored along with the key.  The dictionary
is one of the most important and frequently used data structures in higher level
programming.  Here are some simple examples of its use in Python.

```python
classroom = {} # Create an empty dictionary (dict)
# Set values in the dict:
classroom['Cory'] = 80
classroom['Ross'] = 90
classroom['Gordon'] = 95
print(classroom)
# Get values in the dict:
print(classroom['Cory'])
print(list(classroom.items()))
print(list(classroom.keys()))
print(list(classroom.values()))
# Store a nested dict:
classroom = dict() # Create an empty dictionary (dict)
classroom['Cory'] = {'Grades': [75, 85, 95]}
classroom['Ross'] = {'Grades': [75, 85, 95, 100]}
classroom['Gordon'] = {'Grades': [95, 95]}
# Nested access
print(classroom)
print(classroom['Ross']['Grades'][-1]) # Get the last grade of Ross
```
```
{'Cory': 80, 'Ross': 90, 'Gordon': 95}
80
[('Cory', 80), ('Ross', 90), ('Gordon', 95)]
['Cory', 'Ross', 'Gordon']
[80, 90, 95]
{'Cory': {'Grades': [75, 85, 95]}, 'Ross': {'Grades': [75, 85, 95, 100]}, 'Gordon': {'Grades': [95, 95]}}
100
```

As with the set, getting and setting elements is very quick for a `dict`.

## Control Flow

Python has many of the same exact control flow patterns as C, though they are a
bit easier to read and often not even necessary to accomplish a task.  Python
has something called **comprehensions** for replacing simple loops.  A
comprehension is almost always preferable to a loop if you can get away with
it, so where possible, we will show the alternative comprehension.

### If Statement

The `if` statement works the same as in C, but it is written
quite differently.  Let's take a look at a simple example.

```python
if 3 > 2:
    print('3 > 2?')
    print('duh')
else:
    print('???')
```
```
3 > 2?
duh
```

The first difference is is that the condition, `3 > 2` does
not need to be surrounded with parentheses, though that would
be valid too.

The second difference is that a colon `:` is required after
the condition.

The third difference is that you don't need curly braces `{}`
even for multiple lines.

In Python, unlike C, whitespace actually matters and changes
the meaning of the program.  Python does not use braces `{}`
to group code, and instead relies on the amount of
indentation.

### For Loop

Lets start with a simple motivating problem.  We want to create a list of
the first 10 positive square numbers.  In C, you would create an array of size
10, loop from 1 to 10 and store the square of the loop index in the array.
In Python you can it this way:

```python
lst = [0] * 10 # Create 10 zeros
for n in range(1, 11): # Loop from 1 to 10
    lst[n-1] = n*n

print(lst)
```
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

You could also create an empty list and add elements as you go

```python
lst = [] # Create an empty list
for n in range(1, 11): # Loop from 1 to 10
    lst.append(n*n)

print(lst)
```
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

The reason our last for loop repeated `lst.append(n*n)` but
not `print(lst)` is only because the former was indented under
the loop.  See what happens when we fail to indent properly:

```python
lst = [] # Create an empty list
for n in range(1, 11): # Loop from 1 to 10
    lst.append(n*n)

    print(lst)
```
```
[1]
[1, 4]
[1, 4, 9]
[1, 4, 9, 16]
[1, 4, 9, 16, 25]
[1, 4, 9, 16, 25, 36]
[1, 4, 9, 16, 25, 36, 49]
[1, 4, 9, 16, 25, 36, 49, 64]
[1, 4, 9, 16, 25, 36, 49, 64, 81]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

This example can most easily be done with exactly equivalent
comprehension:

```python
lst = [n*n for n in range(1, 11)]

print(lst)
```
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

This comprehension would certainly be prefered as it is less code and more
easily readable.

### Nested For Loop

Just as in C we can have nested for loops, we can have them in Python as well
with the predictable syntax.  Let's take a look at an example that produces
coordinate tuples in list of lists.

```python
import pprint

a = []
for m in range(5):
    a.append([])
    for n in range(5):
        a[m].append((m, n))

pprint.pprint(a)
```
```
[[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4)],
 [(1, 0), (1, 1), (1, 2), (1, 3), (1, 4)],
 [(2, 0), (2, 1), (2, 2), (2, 3), (2, 4)],
 [(3, 0), (3, 1), (3, 2), (3, 3), (3, 4)],
 [(4, 0), (4, 1), (4, 2), (4, 3), (4, 4)]]
```

Here we are using a list of lists to simulate a 2D array.  We could also create
an array of zeros and then fill in each value rather than appending, like this:

```python
import pprint

a = [[0]*5, [0]*5, [0]*5, [0]*5, [0]*5]
for m in range(5):
    for n in range(5):
        a[m][n] = (m, n)

pprint.pprint(a)
```
```
[[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4)],
 [(1, 0), (1, 1), (1, 2), (1, 3), (1, 4)],
 [(2, 0), (2, 1), (2, 2), (2, 3), (2, 4)],
 [(3, 0), (3, 1), (3, 2), (3, 3), (3, 4)],
 [(4, 0), (4, 1), (4, 2), (4, 3), (4, 4)]]
```

Finally, we could also use a nested list comprehension.

```python
import pprint

a = [[(m, n) for n in range(5)] for m in range(5)]

pprint.pprint(a)
```
```
[[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4)],
 [(1, 0), (1, 1), (1, 2), (1, 3), (1, 4)],
 [(2, 0), (2, 1), (2, 2), (2, 3), (2, 4)],
 [(3, 0), (3, 1), (3, 2), (3, 3), (3, 4)],
 [(4, 0), (4, 1), (4, 2), (4, 3), (4, 4)]]
```

At this point, some may consider the comprehension harder to read than the nested
for loop, but it does save a decent amount of lines.  It is a matter of taste
on which one you should use.

### Continue and Break

The keywords `continue` and `break` carry over with the same exactly behavior
as in C.

This example shows how can you can use `continue` to create a
list of filtered elements.  We add elements from 0 to 99 if
the element is not divisible by any element less

```python
lst = []

for x in range(100):
    if x % 3 or x % 5 == 0:
        continue
    lst.append(x)

print(lst)
```
```
[3, 6, 9, 12, 18, 21, 24, 27, 33, 36, 39, 42, 48, 51, 54, 57, 63, 66, 69, 72, 78, 81, 84, 87, 93, 96, 99]
```

We can achieve similar behavior with a list comprehension as
well.

```python
lst = [x for x in range(100) if x % 3 != 0 and x % 5 != 0]

print(lst)
```
```
[1, 2, 4, 7, 8, 11, 13, 14, 16, 17, 19, 22, 23, 26, 28, 29, 31, 32, 34, 37, 38, 41, 43, 44, 46, 47, 49, 52, 53, 56, 58, 59, 61, 62, 64, 67, 68, 71, 73, 74, 76, 77, 79, 82, 83, 86, 88, 89, 91, 92, 94, 97, 98]
```

Here we use break to find the solution to an equation.

```python
for n in range(100):
    if (n * 342) % 333 == 243:
        break

print(n)
```
```
27
```

Python has an additional, very minor, control flow feature
which is uncommon to other languages.  You can actually attach
an `else` at the end of a `for` loop.  According to the Python
developers, they wished they had called it `ifnobreak` because
that is exactly how it works.  The code inside the `else` on
a `for` loop will trigger if the for loop did not exit via
`break`.  We could use this to detect if we did not find a
solution in the last problem.  For example:

```python
for n in range(100):
    if (n * 342) % 333 == 242:
        print(n)
        break
else:
    print('No solution')
```
```
No solution
```

### While Loop

While loops are basically the same as in C.  Here is a simple
example that counts the number of steps of the Collatz process
to reach 1.  (Minor note: we use `//` here to perform an
integer division which ensures the result will be an integer)

### Functions

Functions are similar to their conterparts in C, but they have
a lot more power.  Lets look at a simple example that just
returns the sum of two numbers.

```python
def plus(a, b):
    return a + b

print(plus(3, 4))
```
```
7
```

The first major difference you'll notice is that you don't
need to have any types associated with the arguments to the
function, or the output.  However, you could add optional
type hints if you want (but they won't do anything).

```python
def plus(a: int, b: int) -> int:
    return a + b

print(plus(3, 4))
```
```
7
```

One nice feature of Python is the ability to return multiple
outputs from a function.  Technically this is not a feature
of functions, but the feature of assigning tuple values to
variables that we saw before.  Let's take a look:

```python
def pythag(maxval):
    for a in range(1, maxval):
        for b in range(1, maxval):
            for c in range(1, maxval):
                if a**2 + b**2 == c**2:
                    return (a, b, c)

    return (None, None, None)

a, b, c = pythag(10)
print(a, b, c)
```
```
3 4 5
```

Note that this is a case where the `None` type is useful
to signal to the caller that a solution could not be found.
In this example we check for that case:

```python
def pythag(maxval):
    for a in range(1, maxval):
        for b in range(1, maxval):
            for c in range(1, maxval):
                if a**2 + b**2 == c**2:
                    return (a, b, c)

    return (None, None, None)

a, b, c = pythag(10)
print(a, b, c)
```
```
3 4 5
```

Note that when checking for `None` values, we use the keyword
`is` rather than `==`.  This just checks that the object is
literally exactly the same as the `None` value.  Normally it
will not make a difference, but it is technically possible
for a custom class to implement custom behavior when comparing
to the `None` value.

#### Varadic Functions

In programming, a **varadic function** is a function which
may take any number of sequential inputs.  For example, let's
say we want to write a function which sums all of its inputs.
This can be done like this:

```python
def sum_inputs(*args):
    total = 0
    for arg in args:
        total += arg

    return total

my_sum = sum_inputs(1, 2, 3)
print(my_sum)
```
```
6
```

You do not have to use the name `args`, you can make that any name you want.
The way this works is that all of the values you feed are put into a list
with the name `args` and you can use that however you want.

This could also be used to ignore or collect extra inputs.

```python
def add(a, b, *args):
    return a + b

my_sum = add(1, 2, 3)
print(my_sum)
```
```
3
```

This can be useful if you are trying to make multiple functions
that have a compatible interface (meaning they can take the same
number of inputs)

You can also use lists to supply the arguments to a function.

```python
def add(a, b):
    return a + b

summands = [1, 2]
my_sum = add(*summands)
print(my_sum)
```
```
3
```

This can be useful for programatically grouping and supplying arguments.

#### Keyword Arugments to Functions

Sometimes functions can take a lot of arguments and it can get
confusing at a first glance as to what argument corresponds
to what parameter.  **Keyword Arguments** allow the programmer
to specify an argument by name rather than by position.  For
example:

```python
def divide(top, bottom):
    return top / bottom

result = divide(1, 5)
print(result)
result = divide(top=1, bottom=5)
print(result)
result = divide(bottom=5, top=1)
print(result)
```
```
0.2
0.2
0.2
```

In case you want to force yourself or another programmer to use
keyword arguments with your function (to avoid common mistakes)
you can place a `*` before the arguments.

```python
def divide(*, top, bottom):
    return top / bottom

result = divide(1, 5)
print(result)
```
```
Traceback (most recent call last):
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/kwargs_2.py", line 4, in <module>
    result = divide(1, 5)
TypeError: divide() takes 0 positional arguments but 2 were given
```

You can automatically gather extra keyword arugments similar to
how you can gather extra positional arguments with `*args` by
using `**kwargs`.  Note again there is nothing special about
the name `kwargs` but it is very commonly used for this case.

```python
def divide(**kwargs):
    return kwargs['top'] / kwargs['bottom']

result = divide(top=1, bottom=5)
print(result)
```
```
0.2
```

Similar to how you can use `*args` when supplying an input
to a function, you can also use `**kwargs` if you want to
supply a dictionary as the input to a function.

```python
def divide(top, bottom):
    return top / bottom

kwargs = {'top': 1, 'bottom': 5}
result = divide(**kwargs)
print(result)
```
```
0.2
```

Combining keyword arugments along with varadic functions, we
can create a function that takes any input at all.

```python
def anything(*args, **kwargs):
    for arg in args:
        print(arg)
    for key, value in kwargs.items():
        print(key, ':', value)

anything(1, 'hello', 5.3, boo='!', whatever=[])
```
```
1
hello
5.3
boo : !
whatever : []
```

We will see later on this pattern is very useful when trying
to modify or extend existing functions, because you can feed
anything into this function that you can into any other function.

### Recursion

Recursion works similarly to C.  Here is a simple Fibonacci
example.

```python
def fib(n):
    if n == 0 or n == 1:
        return 1
    else:
        return fib(n-1) + fib(n-2)

for n in range(10):
    print(fib(n))
```
```
1
1
2
3
5
8
13
21
34
55
```

However there is one weakness: There is a fairly low limit to
how many times you are allowed to recurse in Python.  Usually
only up to a depth of around 1000.  For example:

```python
def count(n):
    if n == 0:
        return 0
    else:
        return 1 + count(n-1)

print(count(100))
print(count(1000))
```
```
100
Traceback (most recent call last):
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/recurse_limit.py", line 8, in <module>
    print(count(1000))
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/recurse_limit.py", line 5, in count
    return 1 + count(n-1)
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/recurse_limit.py", line 5, in count
    return 1 + count(n-1)
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/recurse_limit.py", line 5, in count
    return 1 + count(n-1)
  [Previous line repeated 995 more times]
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/recurse_limit.py", line 2, in count
    if n == 0:
RecursionError: maximum recursion depth exceeded in comparison
```

### Control Flow Conclusion

That all covers basic control flow in Python.  Just to show
a quick example of more meaningful code, here is the
`mandelbrot` assignment re-written in Python.

```python
def in_mandelbrot_set(c):
    x = 0
    for n in range(100):
        x = x*x + c
        if abs(x) > 2:
            return False

    return True

def visualize():
    dx = 0.03125;
    dy = 0.0625;
    for n in range(-16, 16+1):
        for m in range(-64, 16+1):
            if in_mandelbrot_set(m*dx + 1j*n*dy):
                print('*', end='')
            else:
                print(' ', end='')
        print();

visualize()
```
```
                                                                *                
                                                                                 
                                                            *                    
                                                         ******                  
                                                         *******                 
                                                          *****                  
                                                    *************** *            
                                               ***********************  ***      
                                                ***************************      
                                            * ****************************       
                                            *******************************      
                                           **********************************    
                           ** ****        ***********************************    
                           ***********   ************************************    
                         *************** ***********************************     
                     **  *************** **********************************      
*************************************************************************        
                     **  *************** **********************************      
                         *************** ***********************************     
                           ***********   ************************************    
                           ** ****        ***********************************    
                                           **********************************    
                                            *******************************      
                                            * ****************************       
                                                ***************************      
                                               ***********************  ***      
                                                    *************** *            
                                                          *****                  
                                                         *******                 
                                                         ******                  
                                                            *                    
                                                                                 
                                                                *                
```

## Advanced Functions

All of that covered the basic control flow we had in C, but
there is even more available in Python.  In particular,
we can do a lot more with functions.

### Functions as Arguments

Similar to C, we can pass functions as arguments to other functions, but the
syntax is a lot simpler in Python.  Watch this:

```python
def add_one(x):
    return x + 1

def apply_function(f, lst):
    length = len(lst)
    for n in range(length):
        lst[n] = f(lst[n])

lst = [1, 2, 3]
print(lst)
apply_function(add_one, lst)
print(lst)
```
```
[1, 2, 3]
[2, 3, 4]
```

**Question: How can we write the above program as a comprehension?**

### Lambdas

In case we don't have a function readily defined, we can use **lambda** to 
define one on the spot.

```python
def add_one(x):
    return x + 1

def apply_function(f, lst):
    length = len(lst)
    for n in range(length):
        lst[n] = f(lst[n])

lst = [1, 2, 3]
print(lst)
apply_function(add_one, lst)
print(lst)
```
```
[1, 2, 3]
[2, 3, 4]
```

There is basically no difference in doing this compared to defining a function
beforehand, it's just convenient.

```python
def apply_function(f, lst):
    length = len(lst)
    for n in range(length):
        lst[n] = f(lst[n])

lst = [1, 2, 3]
print(lst)
apply_function(lambda x: x + 1, lst)
print(lst)
```
```
[1, 2, 3]
[2, 3, 4]
```

You will often see this in the context of some built in functions:

```python
import pprint
lst = [
    {'name': 'zachary', 'grade': 70},
    {'name': 'cory', 'grade': 80},
    {'name': 'deborah', 'grade': 100},
    {'name': 'ross', 'grade': 90},
    {'name': 'gordon', 'grade': 85},
]
print('Unsorted')
pprint.pprint(lst)
lst.sort(key=lambda record: record['grade'])
print('Sorted by grade')
pprint.pprint(lst)
lst.sort(key=lambda record: record['name'])
print('Sorted by name')
pprint.pprint(lst)
print('Highest Grade')
pprint.pprint(max(lst, key=lambda record: record['grade']))
print('First Name (Alphabetically)')
pprint.pprint(min(lst, key=lambda record: record['name']))
```
```
Unsorted
[{'grade': 70, 'name': 'zachary'},
 {'grade': 80, 'name': 'cory'},
 {'grade': 100, 'name': 'deborah'},
 {'grade': 90, 'name': 'ross'},
 {'grade': 85, 'name': 'gordon'}]
Sorted by grade
[{'grade': 70, 'name': 'zachary'},
 {'grade': 80, 'name': 'cory'},
 {'grade': 85, 'name': 'gordon'},
 {'grade': 90, 'name': 'ross'},
 {'grade': 100, 'name': 'deborah'}]
Sorted by name
[{'grade': 80, 'name': 'cory'},
 {'grade': 100, 'name': 'deborah'},
 {'grade': 85, 'name': 'gordon'},
 {'grade': 90, 'name': 'ross'},
 {'grade': 70, 'name': 'zachary'}]
Highest Grade
{'grade': 100, 'name': 'deborah'}
First Name (Alphabetically)
{'grade': 80, 'name': 'cory'}
```

### Functions as Return Values

We can also create or modify functions and then use or return them.
For example, we can create a function that takes in any other function
as a parameter and then returns a function which does the same thing,
and also prints the time it took to run.

```python
import time

def timed(f):
    def wrapper(*args, **kwargs):
        t1 = time.time()
        retval = f(*args, **kwargs)
        t2 = time.time()
        print(f'Calling "{f.__name__}" took {t2-t1} seconds')
        return retval
    return wrapper

def wait(seconds):
    print('waiting')
    time.sleep(seconds)
    print('done waiting!')

timed_wait = timed(wait)

timed_wait(0.1)
timed_wait(0.2)
timed_wait(0.3)
```
```
waiting
done waiting!
Calling "wait" took 0.10355091094970703 seconds
waiting
done waiting!
Calling "wait" took 0.20382285118103027 seconds
waiting
done waiting!
Calling "wait" took 0.3050539493560791 seconds
```

This is fairly common for some Python programs, so there is even a
special syntax for doing it:

```python
import time

def timed(f):
    def wrapper(*args, **kwargs):
        t1 = time.time()
        retval = f(*args, **kwargs)
        t2 = time.time()
        print(f'Calling "{f.__name__}" took {t2-t1} seconds')
        return retval
    return wrapper

@timed
def wait(seconds):
    print('waiting')
    time.sleep(seconds)
    print('done waiting!')

timed_wait(0.1)
timed_wait(0.2)
timed_wait(0.3)
```
```
Traceback (most recent call last):
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/functional_3.py", line 18, in <module>
    timed_wait(0.1)
NameError: name 'timed_wait' is not defined
```

The `@` basically says to do something like `wait = timed(wait)` just after the
definition.  A function like this, which takes a function and returns a
function is called a **decorator**.

### Generators

In Python, there is a special type of object called a **generator function**.  A
generator function is like a function, except that it maintains state between
calls.  It can maintain data like variables, and even what line of code it
exited from.  It will return to that line of code when you call it again.

Here is a simple generator which counts to 3.

```python
def count_to_3():
    yield 1
    yield 2
    yield 3

generator = count_to_3()
print(next(generator))
print(next(generator))
print(next(generator))
```
```
1
2
3
```

Instead of `return`, you give a value back with `yield`.  You can see that
every time you call `next` on a generator it advances to the next `yield`
statement.  If you go too far, you will get an error.

```python
def count_to_3():
    yield 1
    yield 2
    yield 3

generator = count_to_3()
print(next(generator))
print(next(generator))
print(next(generator))
print(next(generator))
```
```
1
2
3
Traceback (most recent call last):
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/generator_wrong.py", line 10, in <module>
    print(next(generator))
StopIteration
```

You can convert any generator into a plain old list by using `list`.

```python
def count_to_3():
    yield 1
    yield 2
    yield 3

generator = count_to_3()
print(list(generator))
```
```
[1, 2, 3]
```

You can do basically anything you can do with a normal function, and even
create multiple instances of a generator at once:

```python
def count_to_n(n):
    for i in range(n):
        yield i

generator_10 = count_to_n(10)
generator_100 = count_to_n(100)
print(list(generator_10))
print(list(generator_100))
print(list(generator_10))
```
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
[]
```

Just be careful!  Generators come with a huge warning.  Once you've used a value,
that's it.  You cannot get it back again it is forever gone.  That is why when
we print `list(generator_10)` a second time, it is empty.

## Input and (File) Output

You can get command line arguments and inputs by using `sys.argv`.
Here is a simple program that echos the user input back to them
separated by newlines.

### Command Line Input

```python
import sys

for arg in sys.argv:
    print(arg)
```
```
snippets/input_1.py
```

You can get interactive user input with the `input` function.

```python
name = input('Enter your name: ')
print(f'Hello, {name}')
```
```
Enter your name: Hello, Cory
```

**Question: Write a program that prints the sum of user inputs**

### File Input

You can read files by using the `open` keyword.

```python
opened_file = open('README.md')

content = opened_file.read()

print(f'Number of characters: {len(content)}')
words = content.split()
print(f'Number of words: {len(words)}')
lines = content.split('\n')
print(f'Number of lines: {len(lines)}')
print(f'Number of unique words: {len(set(words))}')

opened_file.close()
```
```
Number of characters: 0
Number of words: 0
Number of lines: 1
Number of unique words: 0
```

It is generally good practice to close a file after you are done
using it.  This is so other programs can get access to it.  It
is a common mistake to forget to close it, so in Python you can
using something called a **context manager** which will close it
for you.

```python
with open('README.md') as opened_file:
    content = opened_file.read()
    print(f'Number of characters: {len(content)}')
    words = content.split()
    print(f'Number of words: {len(words)}')
    lines = content.split('\n')
    print(f'Number of lines: {len(lines)}')
    print(f'Number of unique words: {len(set(words))}')
```
```
Number of characters: 0
Number of words: 0
Number of lines: 1
Number of unique words: 0
```

### File Output

You can write to files in a similar way as you read from them.

```python
with open('output.txt', 'w') as opened_file:
    opened_file.write('Hello, ')
    opened_file.write('world')
    opened_file.write('!')

with open('output.txt') as opened_file:
    print(opened_file.read())
```
```
Hello, world!
```

## Classes

### Basic Example

Classes in Python are similar to classes in C++, just with some different
syntax and more freedom.  You can define a new class by using the `class`
keyword, and create a new instance (object) by "calling" it with parentheses.
Here is a simple example.

```python
class Foo():
    pass

foo = Foo()

print(foo)
```
```
<__main__.Foo object at 0x1018a7340>
```

### Methods

Methods of classes can defined the same way functions can.  Just make sure
they are indented and within in your class definition.  One major difference
between Python and C++ (and more languages) is that in Python, the reference
to the object (the `this` keyword in C++) is implicitly provided as an input
to every method.  Here is an example demonstrating this

```python
class Foo():
    def print_hi(self):
        print('hi')

foo = Foo()
foo.print_hi()
```
```
hi
```

The name `self` is not special, you could technically put anything there, but
the name `self` is the convention and there is no reason to stray from it.
You must explicitly type `self` as the first input of every method (with few
exceptions we will talk about later)

Here is an example of a common mistake.  Forgetting to write `self` as the first
argument leads to an error because the method is implicitly called with `foo` as
the first argument but as defined the method takes zero arguments.

```python
class Foo():
    def print_hi():
        print('hi')

foo = Foo()
foo.print_hi()
```
```
Traceback (most recent call last):
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/method_wrong.py", line 6, in <module>
    foo.print_hi()
TypeError: print_hi() takes 0 positional arguments but 1 was given
```

### Constructor

You can create a constructor for a class by implementing the special
`__init__` method.  The double underscores preceding and following `init`
can be pronounced **dunder**, so we can pronounce this as **dunder init**.
This method is known as a **magic method** because it is typically not
called explicitly.  Here is an example of a simple constructor.

```python
class Foo():

    def __init__(self, x):
        self.x = x

    def print_x(self):
        print(self.x)

foo = Foo(5)
foo.print_x()
```
```
5
```

Note that as with other methods, `self` is the first argument.  We can
use `self` to add data to the object.  In this cases we added some 
arbitrary `x` value, and then we can reference it later in `print_x`

### Destructor

You don't really have to write destructors in Python because memory is
mostly handled for you.  However the option is there with the magic method
`__del__` which we can see implemented here

```python
class Foo():

    def __init__(self, x):
        self.x = x

    def print_x(self):
        print(self.x)

    def __del__(self):
        print('I am being destroyed')

foo = Foo(5)
foo.print_x()
print('getting rid of foo')
foo = 1
print('got rid of foo')
```
```
5
getting rid of foo
I am being destroyed
got rid of foo
```

You can see that we never explicitly delete the object like in C++, we just
set the variable name containing that object to another variable and Python is
smart enough to destroy the object when it sees we may no longer reference it.

### Static Methods

If the method you are writing does not need a reference to the object calling it,
but you want to logically group it with your class, you can use the `@staticmethod`
decorator to avoid passing `self` like this:

```python
class Foo():
    @staticmethod
    def print_hi():
        print('hi')

foo = Foo()
foo.print_hi()
Foo.print_hi()
```
```
hi
hi
```

In this case, you should consider whether it makes sense to just move the
function out of the class, since it has the same effect.

**Problem:** How can we implement the `@staticmethod` deocrator?

### Class Methods

If you want to write a method which creates an instance of your class with
some special logic, you can use a `@classmethod`.  In a class method, the
class of the object will be implicitly given as the first paremeter, rather
than the object itself.  This can useful for creating classes from some
other common objects with some additional logic.  Here is an example.

```python
class Foo():
    def __init__(self, one, two, three):
        self.one = one
        self.two = two
        self.three = three

    def print_all(self):
        print(self.one, self.two, self.three)

    @classmethod
    def make_foo_from_list(cls, lst):
        return cls(lst[0], lst[1], lst[2])

foo = Foo.make_foo_from_list(['a', 'b', 'c'])
foo.print_all()
```
```
a b c
```

### Abstract Methods

Python has **abstract base classes** and **virtual functions**, almost the same
as in C++ but under some new syntax and naming.  Here is an example that
implements an abstract base class with one virtual function (now called an
abstract method)

```python
import abc # abstract base class

class Foo(abc.ABC):
    @abc.abstractmethod
    def print_me():
        pass

foo = Foo()
```
```
Traceback (most recent call last):
  File "/Users/cnezin/cs102/Lesson-7-Introduction-To-Python/snippets/abstractmethod.py", line 8, in <module>
    foo = Foo()
TypeError: Can't instantiate abstract class Foo with abstract method print_me
```

You can see if we try to create an instance of an abstract base class that
has an abstract method, we get an error, as we did in C++.  We can fix this
by creating a new class and **inheriting** from the base class, implementing
the method.

```python
import abc # abstract base class

class Foo(abc.ABC):
    @abc.abstractmethod
    def print_me(self):
        pass

class XBar(Foo):
    def __init__(self, x):
        self.x = x

    def print_me(self):
        print(self.x.lower())

class YBar(Foo):
    def __init__(self, y):
        self.y = y

    def print_me(self):
        print(self.y.upper())

xbar = XBar('xyz')
ybar = YBar('xyz')
xbar.print_me()
ybar.print_me()
```
```
xyz
XYZ
```

### Inheritance

Inheritance works pretty much the same as in C++, let's take a look at an example.

```python
import abc # abstract base class

class Foo():
    def print_hi(self):
        print('hi')
    def print_bye(self):
        print('bye')

class Bar(Foo):
    def print_hi(self):
        print('hello there')

foo = Foo()
foo.print_hi()
foo.print_bye()
bar = Bar()
bar.print_hi()
bar.print_bye()
```
```
hi
bye
hello there
bye
```

You can use the `super` keyword to call a parent method, when implementing a new
version of that method.  For example, let's say we wanted to extend a class's
constructor to take an additional parameter but otherwise do the same stuff.

### Other Magic Methods

There are a ton of other magic methods that Python lets you override in your
classes.  Here we will go over an example with a couple, but there are a lot
more.

```python
class Interval():
    def __init__(self, start, end):
        self.start = start
        self.end = end

    def __repr__(self):
        return f'{self.start} -> {self.end}'

    def __str__(self):
        return f'{self.start} -> {self.end}'

    def __contains__(self, element):
        return bool(self.start < element < self.end)

    def __iter__(self):
        return iter(range(self.start, self.end + 1))

    def __mul__(self, other):
        return Interval(max(self.start, other.start), min(self.end, other.end))

    def __nonzero__(self):
        return bool(len(self))

    def __len__(self):
        return self.end - self.start

foo = Interval(5, 9)
bar = Interval(7, 11)
empty = Interval(7, 7)
print(foo)
print(6 in foo)
print(list(foo))
print(foo * bar)
print(len(empty))
print(bool(empty))
```
```
5 -> 9
True
[5, 6, 7, 8, 9]
7 -> 9
0
False
```
