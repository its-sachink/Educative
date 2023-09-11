# Exceptions :

1. What is an exception? Usually it’s an error, an indication that something went wrong. (Not all exceptions are errors, but never mind that for now.) Some programming languages encourage the use of error return codes, which you check. Python encourages the use of exceptions, which you handle.
</br>
</br>
2. When the exception was raised, there was no code to explicitly notice it and deal with it, so it bubbled its way back up to the top level of the Python Shell, which spits out some debugging information and calls it a day.
</br>
</br>
3. When the exception was raised, there was no code to explicitly notice it and deal with it, so it bubbled its way back up to the top level of the Python Shell, which spits out some debugging information and calls it a day.
</br>
</br>
If you know a line of code may raise an exception, you should handle the exception using a <mark>try...except</mark> block.
</br>
</br>
4. The approximate_size() function raises exceptions in two different cases: if the given size is larger than the function is designed to handle, or if it’s less than zero.

```python
if size < 0:
    raise ValueError('number must be non-negative')
```
Use the <mark>raise</mark> statement, followed by the exception name, and an optional human-readable string for debugging purposes.

You don’t need to handle an exception in the function that raises it. If one function doesn’t handle it, the exception is passed to the calling function, then that function’s calling function, and so on “up the stack.” If the exception is never handled, your program will crash, Python will print a “traceback” to standard error, and that’s the end of that. Again, maybe that’s what you want; it depends on what your program does.
</br>
</br>

## Catching Import Errors :

Python’s built-in exceptions is <em>**ImportError**</em>, which is raised when you try to import a module and fail. This can happen for a variety of reasons, but the simplest case is when the module doesn’t exist in your import search path.
</br>
</br>
Your program wants to use this library if it exists, but continue gracefully if the user hasn’t installed it. You can do this with a try..except block.
```python
try:
  import chardet
except ImportError:
  chardet = None
```
Later, you can check for the presence of the chardet module with a simple if statement:
```python
if chardet:
  # do something
else:
  # continue anyway
```

You can try to import one module but fall back to a different module if the first import fails. For example, the XML chapter talks about two modules that implement a common **API**, called the **ElementTree API**. The first, **lxml**, is a third-party module that you need to download and install yourself. The second, **xml.etree.ElementTree**, is slower but is part of the Python 3 standard library.

```python
try:
    from lxml import etree
except ImportError:
    import xml.etree.ElementTree as etree
```

By the end of this try..except block, you have imported some module and named it etree. Since both modules implement a common API, the rest of your code doesn’t need to keep checking which module got imported. 
</br>
</br>
And since the module that did get imported is always called etree, the rest of your code doesn’t need to be littered with if statements to call differently-named modules.
</br>
</br>
</br>
</br>

## Few more important points : 
</br>
</br>
### 1. Unbound Variables :
</br>
```python
multiple = 1024 if a_kilobyte_is_1024_bytes else 1000
```

You never declare the variable multiple, you just assign a value to it. That’s OK, because Python lets you do that. <mark>What Python will not let you do is reference a variable that has never been assigned a value.</mark> Trying to do so will raise a **NameError** exception.

```python
x
#Traceback (most recent call last):
#  File "/usercode/__ed_file.py", line 1, in <module>
# x
#NameError: name 'x' is not defined
```
</br>
</br>

### 2. Everything is Case-Sensitive :
</br>
All names in Python are case-sensitive: variable names, function names, class names, module names, exception names. If you can get it, set it, call it, construct it, import it, or raise it, it’s case-sensitive.

```python
an_integer = 1
print (an_integer)
#1
```
</br>

```python
AN_INTEGER
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 1, in <module>
# AN_INTEGER
#NameError: name 'AN_INTEGER' is not defined
```
</br>

```python
An_Integer
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 1, in <module>
# An_Integer
#NameError: name 'An_Integer' is not defined
```


### 3. Running Scripts :
</br>

```python
from humansize import approximate_size

if __name__ == '__main__':
    print(approximate_size(1000000000000, False))
    print(approximate_size(1000000000000))
```
</br>
</br>

Modules are objects, and all modules have a built-in attribute \___name\__. A module’s \___name\__ depends on how you’re using the module. If you import the module, then \___name\__ is the module’s filename, without a directory path or file extension.

```python
import humansize
print(humansize.__name__)
#humansize
```

But you can also <mark>**run the module directly as a standalone program**</mark>, in which case \___name\__ will be a special default value, \___main\__. Python will evaluate this if statement, find a true expression, and execute the if code block. In this case, to print two values.