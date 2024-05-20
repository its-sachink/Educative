


##  Instantiating Classes :

- To instantiate a class, simply call the class as if it were a function, passing the arguments that the __init__() method requires.
- The return value will be the newly created object.

``` python
import fibonacci2
fib = fibonacci2.Fib(100)          #①
print (fib)                        #②
#<fibonacci2.Fib object at 0x7f7594e75ba8>

print (fib.__class__)              #③
#<class 'fibonacci2.Fib'>

print (fib.__doc__ )               #④
#iterator that yields numbers in the Fibonacci sequence
```

- ① You are creating an instance of the Fib class (defined in the fibonacci2 module) and assigning the newly created instance to the variable fib. You are passing one parameter, 100.
- ② fib is now an instance of the Fib class.
- ③ Every class instance has a built-in attribute, __class__, which is the object’s class. Java programmers may be familiar with the Class class, which contains methods like getName() and getSuperclass().
- ④ You can access the instance’s docstring just as with a function or a module. All instances of a class share the same docstring.



## Instance Variables :

``` python
class Fib:
    def __init__(self, max):
        self.max = max        #①
```

- ① What is self.max? It’s an instance variable. It is completely separate from max, which was passed into the __init__() method as an argument. self.max is “global” to the instance. **That means that you can access it from other methods.**

``` python
import fibonacci2
fib1 = fibonacci2.Fib(100)
fib2 = fibonacci2.Fib(200)

print (fib1.max)
#100
print (fib2.max)
#200
```

- Instance variables are specific to one instance of a class. For example, if you create two Fib instances with different maximum values, they will each remember their own values.

</br>