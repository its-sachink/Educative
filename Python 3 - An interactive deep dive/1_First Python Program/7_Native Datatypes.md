# Native Datatypes :

</br>
</br>

## 1. Diving In:
</br>


Python has many native datatypes. Here are the important ones:

1. **Booleans** are either True or False.
2. **Numbers** can be integers (1 and 2), floats (1.1 and 1.2), fractions (1/2 and 2/3), or even complex numbers.
3. **Strings** are sequences of Unicode characters, e.g. an HTML document.
4. **Bytes** and byte arrays, e.g. a JPEG image file.
5. **Lists** are ordered sequences of values.
6. **Tuples** are ordered, immutable sequences of values.
7. **Sets** are unordered bags of values.
8. **Dictionaries** are unordered bags of key-value pairs.
</br>
</br>
Everything is an object in Python, so there are types like module, function, class, method, file, and even compiled code.
</br>
</br>

### Booleans:
</br>
1. snippet from humansize.py:
</br>
</br>

```python
if size < 0:
    raise ValueError('number must be non-negative')
```
- Further
```python
size = 1
print (size < 0)
#False

size = 0
print (size < 0)
#False

size = -1
print (size < 0)
#True
```
- Booleans can also be treated as numbers :
```python
print (True + True)
#2

print (True - False)
#1

print (True * False)
#0

print (True / False)

#Traceback (most recent call last):
#   File "/usercode/__ed_file.py", line 10, in <module>
# print (True / False)
#ZeroDivisionError: division by zero
```

</br>
</br>

### Numbers :

</br>
- Integer type :

```python
print (type(1))                 #①
#<class 'int'>

print (isinstance(1, int) )     #②
#True

print (1 + 1 )                  #③
#2

print (1 + 1.0 )                #④
#2.0

print (type(2.0))
#<class 'float'>
```

- Type casting Integer to Float :

```python
print (float(2) )               #①
#2.0

print (int(2.0))                #②
#2

print (int(2.5) )               #③
#2

print (int(-2.5) )              #④
#-2

print (1.12345678901234567890)  #⑤
#1.1234567890123457

print (type(1000000000000000))  #⑥
#<class 'int'>
```

- Common Numberical Operations

```python
print (11 / 2)      #①
#5.5

print (11 // 2)     #②
#5

x = -11
print ( x // 2)     #③
#−6

print (11.0 // 2)   #④
#5.0

print (11 ** 2)     #⑤
#121

print (11 % 2)      #⑥
#1
```
</br>
</br>
- Fractions :

```python
import fractions                      #①
x = fractions.Fraction(1, 3)          #②
print (x)
#Fraction(1, 3)

print (x * 2 )                        #③
#Fraction(2, 3)

print (fractions.Fraction(6, 4))      #④
#Fraction(3, 2)

print (fractions.Fraction(0, 0) )     #⑤
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 12, in <module>
# print (fractions.Fraction(0, 0) ) #\u2464
# File "/usr/lib/python3.4/fractions.py", line 167, in __new__
# raise ZeroDivisionError('Fraction(%s, 0)' % numerator)
#ZeroDivisionError: Fraction(0, 0)
```
</br>

- output

```
1/3
2/3
3/2
```

</br>
</br>
- Trigonometry :

```python
import math
print (math.pi )               #①
#3.141592653589793

print (math.sin(math.pi / 2))  #②
#1.0

print (math.tan(math.pi / 4))  #③
#0.99999999999999989
```
</br>
</br>
- Numbers In A Boolean Context :

```python
def is_it_true(anything):             #①
   if anything:
     print("yes, it's true")
   else:
     print("no, it's false")


print (is_it_true(1) )                #②
#yes, it's true
#None

print (is_it_true(-1))
#yes, it's true
#None

print (is_it_true(0))
#no, it's false
#None

print (is_it_true(0.1) )                      #③
#yes, it's true
#None

print (is_it_true(0.0))
#no, it's false
#None

import fractions
print (is_it_true(fractions.Fraction(1, 2)))  #④
#yes, it's true
#None

print (is_it_true(fractions.Fraction(0, 1)))
#no, it's false
#None
```
