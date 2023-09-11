# Tuples:

### - Creating a List :
</br>

***A <mark>tuple is an immutable list</mark>. A tuple can not be changed in any way once it is created.***
</br>

```python
a_tuple = ("a", "b", "mpilgrim", "z", "example")          #①
print (a_tuple)
#('a', 'b', 'mpilgrim', 'z', 'example')

print (a_tuple[0] )                                       #②
#a

print (a_tuple[-1])                                       #③
#example

print (a_tuple[1:3] )                                     #④
#('b', 'mpilgrim')
```

1. Whole set of elements is enclosed in **parentheses** instead of square brackets.

2. Slicing works too, just like a list. When you slice a list, you get a new list; when you slice a tuple, you get a new tuple.

3. The major difference between tuples and lists is that **tuples can not be changed**. In technical terms, tuples are immutable.
</br>

    Lists have methods like append(), extend(), insert(), remove(), and pop(). Tuples have none of these methods.

```python
# continued from the previous example
a_tuple = ("a", "b", "mpilgrim", "z", "example")
print (a_tuple)
#('a', 'b', 'mpilgrim', 'z', 'example')

print (a_tuple.append("new"))               #①
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 6, in <module>
# print (a_tuple.append("new")) #\u2460
#AttributeError: 'tuple' object has no attribute 'append'
```

#### Index Function :
</br>

```python
a_tuple = ("a", "b", "mpilgrim", "z", "example")

print (a_tuple.index("example") )           #③
#4

print ("z" in a_tuple)                      #④
#True
```

### So what are tuples good for?

1. **Tuples are faster than lists**. If you’re defining a constant set of values and all you’re ever going to do with it is iterate through it, use a tuple instead of a list. </br>

2. It makes your code safer if you **“write-protect”** data that doesn’t need to be changed. Using a tuple instead of a list is like having an implied assert statement that shows this data is constant
</br>

3. Some **tuples can be used as dictionary keys**(specifically, tuples that contain immutable values like strings, numbers, and other tuples). **Lists can never be used as dictionary keys, because lists are not immutable.**
</br>
</br>
</br>
</br>

### Tuples In A Boolean Context :

```python
def is_it_true(anything):
   if anything:
     print("yes, it's true")
   else:
     print("no, it's false")

print (is_it_true(()))             #①
#no, it's false
#None

print (is_it_true(('a', 'b')))     #②
#yes, it's true
#None

print (is_it_true((False,)))       #③
#yes, it's true
#None

print (type((False)))              #④
#<class 'bool'>

print (type((False,)))
#<class 'tuple'>
```
</br>
</br>
</br>
</br>

### Assigning Multiple Values At Once :
</br>

1. Example 1:
```python
v = ('a', 2, True)
(x, y, z) = v       #①
print (x)
#a

print (y)
#2

print (z)
#True
```
</br>

2. Example 2:


```python
(MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY) = range(7)  #①

print (MONDAY)                                                               #②
#0

print (TUESDAY)
#1

print (SUNDAY)
#6
```




