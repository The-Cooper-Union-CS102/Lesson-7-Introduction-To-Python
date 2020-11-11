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
that is exactly how it works.  The code inside the `else` for
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

Similar to C, we can pass functions as arguments to other
functions, but the syntax is a lot simpler in Python.
