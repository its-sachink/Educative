# Declaring Functions

```python
def approximate_size(size, a_kilobyte_is_1024_bytes=True):
```

- Python functions do not specify the datatype of their return value; they don’t even specify whether or not they return a value. (In fact, every Python function returns a value; <mark>if the function ever executes a return statement, it will return that value, otherwise it will return None, the Python null value.) </mark>

- Python, variables are never explicitly typed. Python figures out what type a variable is and keeps track of it internally.


## Optional and named arguments

- Python allows function arguments to have default values; <mark>if the function is called without the argument, the argument gets its default value. Furthermore, arguments can be specified in any order by using named arguments. </mark>

- Let’s take another look at that approximate_size() function declaration:

```python
def approximate_size(size, a_kilobyte_is_1024_bytes=True):
```

<mark>The second argument, a_kilobyte_is_1024_bytes, specifies a default value of True. This means the argument is optional; you can call the function without it</mark>, and Python will act as if you had called it with True as a second parameter.


<br>

- Now look at the bottom of the script:

```python
if __name__ == '__main__':
    print(approximate_size(1000000000000, False))  # ①
    print(approximate_size(1000000000000))         # ②
```

① This calls the approximate_size() function with two arguments. Within the approximate_size() function, a_kilobyte_is_1024_bytes will be False, since you explicitly passed False as the second argument.

② <mark> This calls the approximate_size() function with only one argument. </mark> But that’s OK, because the second argument is optional! Since the caller doesn’t specify,<mark> the second argument defaults to True, as defined by the function declaration.</mark>

</br>
</br>
</br>
You can also pass values into a function by name.
</br>
</br>

## Program 1
```python
from humansize import approximate_size
print (approximate_size(4000, a_kilobyte_is_1024_bytes=False))       #①
#'4.0 KB'
```

</br>
</br>

## Program 2
```python
from humansize import approximate_size
print(approximate_size(size=4000, a_kilobyte_is_1024_bytes=False))   #②
#'4.0 KB'
```
These named arguments happen to be in the same order as the arguments are listed in the function declaration, but that doesn’t matter either.

</br>
</br>

## Program 3
```python
from humansize import approximate_size
print (approximate_size(a_kilobyte_is_1024_bytes=False, size=4000))  #③
#'4.0 KB'
```
③ This calls the approximate_size() function with False for the argument named a_kilobyte_is_1024_bytes and 4000 for the argument named size. (See? I told you the order didn’t matter.)

</br>
</br>

## Program 4
```python
from humansize import approximate_size

print (approximate_size(a_kilobyte_is_1024_bytes=False, 4000))       #④
# File "/usercode/__ed_file.py", line 11
# print (approximate_size(a_kilobyte_is_1024_bytes=False, 4000)) #\u2463
# ^
#SyntaxError: non-keyword arg after keyword arg
```

④ This call fails, because you have a named argument followed by an unnamed (positional) argument, and that never works. Reading the argument list from left to right,<mark> once you have a single named argument, the rest of the arguments must also be named. </mark>

</br>
</br>

## Program 5
```python
from humansize import approximate_size

print (approximate_size(size=4000, False) )                          #⑤
# File "/usercode/__ed_file.py", line 3
# print (approximate_size(size=4000, False) ) 
# ^
#SyntaxError: non-keyword arg after keyword arg
```
you passed 4000 for the argument named size, then “obviously” that False value was meant for the a_kilobyte_is_1024_bytes argument. But Python doesn’t work that way. <mark>As soon as you have a named argument, all arguments to the right of that need to be named arguments, too. </mark>





