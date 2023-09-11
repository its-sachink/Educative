# Lists:

### - Creating a List :
</br>

```python
a_list = ['a', 'b', 'mpilgrim', 'z', 'example']          #①
print (a_list)
#['a', 'b', 'mpilgrim', 'z', 'example']

print (a_list[0] )                                       #②
#a

print (a_list[4] )                                       #③
#example

print (a_list[-1])                                       #④
#example

print (a_list[-3])                                       #⑤
#mpilgrim
```


### - Slicing a List:
</br>

- Once you’ve defined a list, you can get any part of it as a new list. This is called slicing the list.
</br>

```python
a_list = ['a', 'b', 'mpilgrim', 'z', 'example'] 

print (a_list)
#['a', 'b', 'mpilgrim', 'z', 'example']

print (a_list[1:3] )           #①
#['b', 'mpilgrim']

print (a_list[1:-1])           #②
#['b', 'mpilgrim', 'z']

print (a_list[0:3] )           #③
#['a', 'b', 'mpilgrim']

print (a_list[:3])             #④
#['a', 'b', 'mpilgrim']

print (a_list[3:] )            #⑤
#['z', 'example']

print (a_list[:] )             #⑥
#['a', 'b', 'mpilgrim', 'z', 'example']
```

- Slicing returns a new list containing all the items of the list, in order, starting with the first slice index (in this case a_list[1]), up to but not including the second slice index (in this case a_list[3]).
- you can think of it this way: reading the list from left to right, **<mark>the first slice index specifies the first item you want, and the second slice index specifies the first item you don’t want. </mark>**

</br>
</br>

### - Adding items to a list:
</br>

- 4 ways to add items to lists:

```python
a_list = ['a']
a_list = a_list + [2.0, 3]          #①
print (a_list )                     #②
#['a', 2.0, 3]

a_list.append(True)                 #③
print (a_list)
#['a', 2.0, 3, True]

a_list.extend(['four', '/'])        #④
print (a_list)
#['a', 2.0, 3, True, 'four', 'Ω']

a_list.insert(0, '/')               #⑤
print (a_list)
#['Ω', 'a', 2.0, 3, True, 'four', 'Ω']
```

- If memory is a concern, you should be aware that list concatenation creates a second list in memory.
- A list can contain items of any datatype, and the items in a single list don’t all need to be the same type.
- The append() method adds a single item to the end of the list.
- The extend() method takes one argument, a list, and appends each of the items of the argument to the original list.
- The insert() method inserts a single item into a list.
</br>
</br>

Difference between append() and extend().
```python
a_list = ['a', 'b', 'c']
a_list.extend(['d', 'e', 'f'])                  #①
print (a_list)
#['a', 'b', 'c', 'd', 'e', 'f']

print (len(a_list))                             #②
#6

print (a_list[-1])
#'f'

a_list.append(['g', 'h', 'i'])                  #③
print (a_list)
#['a', 'b', 'c', 'd', 'e', 'f', ['g', 'h', 'i']]

print (len(a_list))                             #④
#7

print (a_list[-1])
#['g', 'h', 'i']
```
-   The extend() method takes a single argument, which is always a list, and adds each of the items of that list to a_list.
-   the append() method takes a single argument, which can be any datatype. Here, you’re calling the append() method with a list of three items.

</br>
</br>
### - Searching for values in a list:

</br>

```python
a_list = ['a', 'b', 'new', 'mpilgrim', 'new']
print (a_list.count('new'))       #①
#2

print ('new' in a_list)           #②
#True

print ('c' in a_list)
#False

print (a_list.index('mpilgrim'))  #③
#3

print (a_list.index('new'))       #④
#2

print (a_list.index('c') )        #⑤
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 17, in <module>
# print (a_list.index('c') ) #\u2464
#ValueError: 'c' is not in list
```

</br>
</br>

### - Removing items from a list:
</br>

- Lists can expand and contract automatically.
</br>

```python
a_list = ['a', 'b', 'new', 'mpilgrim', 'new']
print (a_list[1])
#'b'

del a_list[1]                 #①
print (a_list)
#['a', 'new', 'mpilgrim', 'new']

print (a_list[1])             #②
#new
```

</br>
- You can also remove items by value instead.

```python
a_list = ['a', 'new', 'mpilgrim', 'new']
a_list.remove('new')                      #①
print (a_list)
#['a', 'mpilgrim', 'new']

a_list.remove('new')                      #②
print (a_list)
#['a', 'mpilgrim']

print (a_list.remove('new'))
#Traceback (most recent call last):
#  File "/usercode/__ed_file.py", line 10, in <module>
# print (a_list.remove('new'))
#ValueError: list.remove(x): x not in list
```


</br>
</br>

### - Removing items from a list: bonus round
</br>

```python
a_list = ['a', 'b', 'new', 'mpilgrim']
print (a_list.pop())   #①
#mpilgrim

print (a_list)
#['a', 'b', 'new']

print (a_list.pop(1) ) #②
#b

print (a_list)
#['a', 'new']

print (a_list.pop())
#new

print (a_list.pop())
#a

print (a_list.pop())   #③
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 20, in <module>
# print (a_list.pop()) #\u2462
#IndexError: pop from empty list
```


</br>
</br>

### - Lists in a boolean context
</br>

```python
def is_it_true(anything):
   if anything:
     print("yes, it's true")
   else:
     print("no, it's false")

print (is_it_true([]) )            #①
#no, it's false
#None

print (is_it_true(['a']))          #②
#yes, it's true
#None

print (is_it_true([False]) )       #③
#yes, it's true
#None
```