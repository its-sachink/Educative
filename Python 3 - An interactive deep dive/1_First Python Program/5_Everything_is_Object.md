# Everything Is An Object

- Python functions have attributes, and that those attributes are available at runtime. <mark>A function, like everything else in Python, is an object. </mark>

```python
import humansize                               #①

print(humansize.approximate_size(4096, True))  #②
#4.0 KiB

print(humansize.approximate_size.__doc__)      #③
#Convert a file size to human-readable form.

#    Keyword arguments:
#    size -- file size in bytes
#    a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024
#                                if False, use multiples of 1000

#    Returns: string
```
</br>
</br>
- ① The first line imports the humansize program as a module — a chunk of code that you can use interactively, or from a larger Python program. Once you import a module, you can reference any of its public functions, classes, or attributes.
- ② When you want to use functions defined in imported modules, you need to include the module name. So you can’t just say approximate_size; it must be humansize.approximate_size.


</br>
</br>
</br>
</br>

## What’s An Object?
</br>
- Everything in Python is an object, and everything can have attributes and methods. All functions have a built-in attribute __doc__, which returns the 'docstring' defined in the function’s source code.
</br>
</br>
In Python, the definition is looser. Some objects have neither attributes nor methods, but they could. Not all objects are subclassable. But everything is an object in the sense that it can be assigned to a variable or passed as an argument to a function.
</br>
</br>
You may have heard the term “first-class object” in other programming contexts. 

1. In Python, `functions` are 'first-class objects'. You can pass a function as an argument to another function. 
2. `Modules` are first-class objects. You can pass an entire module as an argument to a function. 
3. `Classes` are first-class objects, and individual instances of a class are also first-class objects.
</br>
</br>
`everything in Python is an object`. `Strings` are objects. `Lists` are objects. `Functions` are objects. `Classes` are objects. `Class instances` are objects. Even `modules` are objects.







