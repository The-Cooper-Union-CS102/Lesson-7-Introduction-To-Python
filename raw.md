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

```snippet
{"code": "snippets/output.py"}
```

## Basic Types

The built in Python types are fairly similar to the built in C types, but we do
get some more functionality as well.  Let's take a look.

### `int`

Integers are mostly the same in Python, with one beautiful exception: they never
oerflow!  For example, take a look at the result of this operation which would
certainly overflow on any built in C integer:

```snippet
{"code": "snippets/bigint.py"}
```

By the way, the `**` in that example is exponentiation.

### `float`

Floats again, are very similar to their C counterparts.  The exception is that
really there is no such thing as a 32-bit float in Python.  Everything is a
64-bit double.  That means they are still susceptible to underflow and overflow
just as they were in C.

```snippet
{"code": "snippets/float.py"}
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

```snippet
{"code": "snippets/string.py"}
```

Formatting strings is way easier in Python.  Here are some different
ways you can format a string

```snippet
{"code": "snippets/format.py"}
```

### Tuple

A tuple is similar to an array in C, with they key exception that it is
**immutable** (again meaning it can not be modified once created) and that
it can store any number of different types.

```snippet
{"code": "snippets/tuple.py"}
```

Note in the above case, the parentheses are not necessary,
the same program would work fine removing them.

```snippet
{"code": "snippets/tuplebad.py"}
```

One nice Python feature is tuple assignment.  If you have a
tuple containing N elements, you can easily assign the
values to N variables like so:

```snippet
{"code": "snippets/tupleassign.py"}
```

This applies with any tuple stored in variables as well,
for example:

```snippet
{"code": "snippets/tupleassignvar.py"}
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

```snippet
{"code": "snippets/list.py"}
```

### Set

A set is a data structure that allows very quick look up for elements.  It has
similar semantics as a list, except it is unordered and faster in most cases.

```snippet
{"code": "snippets/sets.py"}
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

```snippet
{"code": "snippets/setbad.py"}
```

Sets have no alternative in C, except if you code the data structure itself.
If you want to learn how a set works under the hood, take the data structures
and algorithms class.

### Dictionary (Hash Table)

A dictionary (which is really the more well-known "hash table") is very similar
to a set, except that a value is also stored along with the key.  The dictionary
is one of the most important and frequently used data structures in higher level
programming.  Here are some simple examples of its use in Python.

```snippet
{"code": "snippets/dictionary.py"}
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

```snippet
{"code": "snippets/if1.py"}
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

```snippet
{"code": "snippets/for1.py"}
```

You could also create an empty list and add elements as you go

```snippet
{"code": "snippets/for2.py"}
```

The reason our last for loop repeated `lst.append(n*n)` but
not `print(lst)` is only because the former was indented under
the loop.  See what happens when we fail to indent properly:

```snippet
{"code": "snippets/for2bad.py"}
```

This example can most easily be done with exactly equivalent
comprehension:

```snippet
{"code": "snippets/for3.py"}
```

This comprehension would certainly be prefered as it is less code and more
easily readable.

### Nested For Loop

Just as in C we can have nested for loops, we can have them in Python as well
with the predictable syntax.  Let's take a look at an example that produces
coordinate tuples in list of lists.

```snippet
{"code": "snippets/nestedfor1.py"}
```

Here we are using a list of lists to simulate a 2D array.  We could also create
an array of zeros and then fill in each value rather than appending, like this:

```snippet
{"code": "snippets/nestedfor2.py"}
```

Finally, we could also use a nested list comprehension.

```snippet
{"code": "snippets/nestedfor3.py"}
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

```snippet
{"code": "snippets/continue.py"}
```

We can achieve similar behavior with a list comprehension as
well.

```snippet
{"code": "snippets/listfilter.py"}
```

Here we use break to find the solution to an equation.

```snippet
{"code": "snippets/break.py"}
```

Python has an additional, very minor, control flow feature
which is uncommon to other languages.  You can actually attach
an `else` at the end of a `for` loop.  According to the Python
developers, they wished they had called it `ifnobreak` because
that is exactly how it works.  The code inside the `else` on
a `for` loop will trigger if the for loop did not exit via
`break`.  We could use this to detect if we did not find a
solution in the last problem.  For example:

```snippet
{"code": "snippets/forelse.py"}
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

```snippet
{"code": "snippets/function1.py"}
```

The first major difference you'll notice is that you don't
need to have any types associated with the arguments to the
function, or the output.  However, you could add optional
type hints if you want (but they won't do anything).

```snippet
{"code": "snippets/function_type_hint.py"}
```

One nice feature of Python is the ability to return multiple
outputs from a function.  Technically this is not a feature
of functions, but the feature of assigning tuple values to
variables that we saw before.  Let's take a look:

```snippet
{"code": "snippets/function_return_multi.py"}
```

Note that this is a case where the `None` type is useful
to signal to the caller that a solution could not be found.
In this example we check for that case:

```snippet
{"code": "snippets/function_return_multi.py"}
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

```snippet
{"code": "snippets/varadic_1.py"}
```

You do not have to use the name `args`, you can make that any name you want.
The way this works is that all of the values you feed are put into a list
with the name `args` and you can use that however you want.

This could also be used to ignore or collect extra inputs.

```snippet
{"code": "snippets/varadic_2.py"}
```

This can be useful if you are trying to make multiple functions
that have a compatible interface (meaning they can take the same
number of inputs)

You can also use lists to supply the arguments to a function.

```snippet
{"code": "snippets/varadic_3.py"}
```

This can be useful for programatically grouping and supplying arguments.

#### Keyword Arugments to Functions

Sometimes functions can take a lot of arguments and it can get
confusing at a first glance as to what argument corresponds
to what parameter.  **Keyword Arguments** allow the programmer
to specify an argument by name rather than by position.  For
example:

```snippet
{"code": "snippets/kwargs_1.py"}
```

In case you want to force yourself or another programmer to use
keyword arguments with your function (to avoid common mistakes)
you can place a `*` before the arguments.

```snippet
{"code": "snippets/kwargs_2.py"}
```

You can automatically gather extra keyword arugments similar to
how you can gather extra positional arguments with `*args` by
using `**kwargs`.  Note again there is nothing special about
the name `kwargs` but it is very commonly used for this case.

```snippet
{"code": "snippets/kwargs_3.py"}
```

Similar to how you can use `*args` when supplying an input
to a function, you can also use `**kwargs` if you want to
supply a dictionary as the input to a function.

```snippet
{"code": "snippets/kwargs_4.py"}
```

Combining keyword arugments along with varadic functions, we
can create a function that takes any input at all.

```snippet
{"code": "snippets/kwargs_5.py"}
```

We will see later on this pattern is very useful when trying
to modify or extend existing functions, because you can feed
anything into this function that you can into any other function.

### Recursion

Recursion works similarly to C.  Here is a simple Fibonacci
example.

```snippet
{"code": "snippets/fibonacci.py"}
```

However there is one weakness: There is a fairly low limit to
how many times you are allowed to recurse in Python.  Usually
only up to a depth of around 1000.  For example:

```snippet
{"code": "snippets/recurse_limit.py"}
```

### Control Flow Conclusion

That all covers basic control flow in Python.  Just to show
a quick example of more meaningful code, here is the
`mandelbrot` assignment re-written in Python.

```snippet
{"code": "snippets/mandelbrot.py"}
```

## Advanced Functions

All of that covered the basic control flow we had in C, but
there is even more available in Python.  In particular,
we can do a lot more with functions.

### Functions as Arguments

Similar to C, we can pass functions as arguments to other functions, but the
syntax is a lot simpler in Python.  Watch this:

```snippet
{"code": "snippets/functional_1.py"}
```

**Question: How can we write the above program as a comprehension?**

### Lambdas

In case we don't have a function readily defined, we can use **lambda** to 
define one on the spot.

```snippet
{"code": "snippets/functional_1.py"}
```

There is basically no difference in doing this compared to defining a function
beforehand, it's just convenient.

```snippet
{"code": "snippets/lambda_1.py"}
```

You will often see this in the context of some built in functions:

```snippet
{"code": "snippets/lambda_2.py"}
```

### Functions as Return Values

We can also create or modify functions and then use or return them.
For example, we can create a function that takes in any other function
as a parameter and then returns a function which does the same thing,
and also prints the time it took to run.

```snippet
{"code": "snippets/functional_2.py"}
```

This is fairly common for some Python programs, so there is even a
special syntax for doing it:

```snippet
{"code": "snippets/functional_3.py"}
```

The `@` basically says to do something like `wait = timed(wait)` just after the
definition.  A function like this, which takes a function and returns a
function is called a **decorator**.

## Input and (File) Output

You can get command line arguments and inputs by using `sys.argv`.
Here is a simple program that echos the user input back to them
separated by newlines.

### Command Line Input

```snippet
{"code": "snippets/input_1.py"}
```

You can get interactive user input with the `input` function.

```snippet
{"code": "snippets/input_2.py",
 "input": "Cory"}
```

**Question: Write a program that prints the sum of user inputs**

### File Input

You can read files by using the `open` keyword.

```snippet
{"code": "snippets/input_3.py"}
```

It is generally good practice to close a file after you are done
using it.  This is so other programs can get access to it.  It
is a common mistake to forget to close it, so in Python you can
using something called a **context manager** which will close it
for you.

```snippet
{"code": "snippets/input_4.py"}
```

### File Output

You can write to files in a similar way as you read from them.

```snippet
{"code": "snippets/output_1.py"}
```

## Classes

### Basic Example

Classes in Python are similar to classes in C++, just with some different
syntax and more freedom.  You can define a new class by using the `class`
keyword, and create a new instance (object) by "calling" it with parentheses.
Here is a simple example.

```snippet
{"code": "snippets/class_1.py"}
```

### Methods

Methods of classes can defined the same way functions can.  Just make sure
they are indented and within in your class definition.  One major difference
between Python and C++ (and more languages) is that in Python, the reference
to the object (the `this` keyword in C++) is implicitly provided as an input
to every method.  Here is an example demonstrating this

```snippet
{"code": "snippets/method.py"}
```

The name `self` is not special, you could technically put anything there, but
the name `self` is the convention and there is no reason to stray from it.
You must explicitly type `self` as the first input of every method (with few
exceptions we will talk about later)

Here is an example of a common mistake.  Forgetting to write `self` as the first
argument leads to an error because the method is implicitly called with `foo` as
the first argument but as defined the method takes zero arguments.

```snippet
{"code": "snippets/method_wrong.py"}
```

### Constructor

You can create a constructor for a class by implementing the special
`__init__` method.  The double underscores preceding and following `init`
can be pronounced **dunder**, so we can pronounce this as **dunder init**.
This method is known as a **magic method** because it is typically not
called explicitly.  Here is an example of a simple constructor.

```snippet
{"code": "snippets/constructor.py"}
```

Note that as with other methods, `self` is the first argument.  We can
use `self` to add data to the object.  In this cases we added some 
arbitrary `x` value, and then we can reference it later in `print_x`

### Destructor

You don't really have to write destructors in Python because memory is
mostly handled for you.  However the option is there with the magic method
`__del__` which we can see implemented here

```snippet
{"code": "snippets/destructor.py"}
```

You can see that we never explicitly delete the object like in C++, we just
set the variable name containing that object to another variable and Python is
smart enough to destroy the object when it sees we may no longer reference it.

### Static Methods

If the method you are writing does not need a reference to the object calling it,
but you want to logically group it with your class, you can use the `@staticmethod`
decorator to avoid passing `self` like this:

```snippet
{"code": "snippets/staticmethod.py"}
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

```snippet
{"code": "snippets/classmethod.py"}
```

### Abstract Methods

Python has **abstract base classes** and **virtual functions**, almost the same
as in C++ but under some new syntax and naming.  Here is an example that
implements an abstract base class with one virtual function (now called an
abstract method)

```snippet
{"code": "snippets/abstractmethod.py"}G
```

You can see if we try to create an instance of an abstract base class that
has an abstract method, we get an error, as we did in C++.  We can fix this
by creating a new class and **inheriting** from the base class, implementing
the method.

```snippet
{"code": "snippets/correct.py"}G
```

### Inheritance

Inheritance works pretty much the same as in C++, let's take a look at an example.

```snippet
{"code": "snippets/inheritance.py"}
```

You can use the `super` keyword to call a parent method, when implementing a new
version of that method.  For example, let's say we wanted to extend a class's
constructor to take an additional parameter but otherwise do the same stuff.

### Other Magic Methods

There are a ton of other magic methods that Python lets you override in your
classes.  Here we will go over an example with a couple, but there are a lot
more.

```snippet
{"code": "snippets/dunder.py"}
```
