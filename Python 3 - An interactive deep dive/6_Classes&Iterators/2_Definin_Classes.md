## Defining Classes :
</br>
- A Python class starts with the reserved word class, followed by the class name.

```python
class PapayaWhip:  #①
    pass           #②
```

- ① The name of this class is PapayaWhip, and it doesn’t inherit from any other class. Class names are usually capitalized, EachWordLikeThis, but this is only a convention, not a requirement.
- ② You probably guessed this, but everything in a class is indented, just like the code within a function.
- This PapayaWhip class doesn’t define any methods or attributes, but syntactically, there needs to be something in the definition, thus the pass statement. This is a Python reserved word that just means “move along, nothing to see here”.

</br>
</br>

### The __init__() Method :

```python
class Fib:
    '''iterator that yields numbers in the Fibonacci sequence'''  #①
    
    def __init__(self, max):                                      #②
        self.max = max     
```

- ① Classes can (and should) have docstrings too, just like modules and functions.
- ② The __init__() method is called immediately after an instance of the class is created. It would be tempting — but technically incorrect — to call this the “constructor” of the class.
    Incorrect, because the object has already been constructed by the time the __init__() method is called, and you already have a valid reference to the new instance of the class.
- The first argument of every class method, including the __init__() method, is always a reference to the current instance of the class. By convention, this argument is named self.
</br>
</br>
</br>