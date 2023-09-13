# Sets :

</br>

***A set is an unordered “bag” of unique values.*** A single set can contain values of any immutable datatype. Once you have two sets, you can do standard set operations like union, intersection, and set difference.

### - Creating A Set :
First things first. Creating a set is easy.

```python

a_set = {1}             #①
print (a_set)
#{1}

print (type(a_set))     #②
#<class 'set'>

a_set = {1, 2}          #③
print (a_set)
#{1, 2}
```
</br>
</br>

1. ② Sets are actually implemented as classes, but don’t worry about that for now.

2. ③ To create a set with multiple values, separate the values with commas and wrap it all up with curly brackets.

3. You can also create a set out of a list.

```python

a_list = ['a', 'b', 'mpilgrim', True, False, 42]
a_set = set(a_list)                                   #①
print (a_set )                                        #②
#{False, True, 'mpilgrim', 'b', 42, 'a'}

print (a_list )                                       #③
#['a', 'b', 'mpilgrim', True, False, 42]

```

1. ② As I mentioned earlier, a single set can contain values of any datatype. And, as I mentioned earlier, sets are unordered. This set does not remember the original order of the list that was used to create it. 
    - If you were to add items to this set, it would not remember the order in which you added them.

2. Don’t have any values yet? Not a problem. You can create an empty set.

```python

a_set = set()            #①
print (a_set )           #②
#set()

print (type(a_set))      #③
#<class 'set'>

print (len(a_set))       #④
#0

print (not_sure = {})    #⑤
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 11, in <module>
# print (not_sure = {}) #\u2464
#TypeError: 'not_sure' is an invalid keyword argument for this function
```

- ① To create an empty set, call set() with no arguments.

-   ⑤ Due to historical quirks carried over from Python 2, you can not create an empty set with two curly brackets. This actually creates an empty dictionary, not an empty set.

</br>
</br>
### - Modifying A Set : 
</br>

There are two different ways to add values to an existing set: the ***add() method, and the update() method***.

```python
a_set = {1, 2}
a_set.add(4)          #①
print (a_set)
#{1, 2, 4}

print (len(a_set))    #②
#3

a_set.add(1)          #③
print (a_set)
#{1, 2, 4}

print (len(a_set))    #④
#3
```

</br>
- ③ Sets are bags of unique values. If you try to add a value that already exists in the set, it will do nothing. It won’t raise an error; it’s just a no-op.

</br>
</br>
</br>
</br>

```python
a_set = {1, 2, 3}
print (a_set)
#{1, 2, 3}

a_set.update({2, 4, 6})                       #①
print (a_set )                                #②
#{1, 2, 3, 4, 6}

a_set.update({3, 6, 9}, {1, 2, 3, 5, 8, 13})  #③
print (a_set)
#{1, 2, 3, 4, 5, 6, 8, 9, 13}

a_set.update([10, 20, 30])                    #④
print (a_set)
#{1, 2, 3, 4, 5, 6, 8, 9, 10, 13, 20, 30}

```
</br>

- ③ You can actually call the update() method with any number of arguments. When called with two sets, the update() method adds all the members of each set to the original set (dropping duplicates).

- ④ The update() method can take objects of a number of different datatypes, including lists. ***<mark>When called with a list, the update() method adds all the items of the list to the original set.*** </mark>


### - Removing Items From A Set :
</br>

There are three ways to remove individual values from a set. The first two, ***discard() and remove()***, have one subtle difference.

```python
a_set = {1, 3, 6, 10, 15, 21, 28, 36, 45}
print (a_set)
#{1, 3, 36, 6, 10, 45, 15, 21, 28}

a_set.discard(10)                        #①
print (a_set)
#{1, 3, 36, 6, 45, 15, 21, 28}

a_set.discard(10)                        #②
print (a_set)
#{1, 3, 36, 6, 45, 15, 21, 28}

a_set.remove(21)                         #③
print (a_set)
#{1, 3, 36, 6, 45, 15, 28}

print (a_set.remove(21))                 #④
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 17, in <module>
# print (a_set.remove(21)) #\u2463
#KeyError: 21

```
</br>

- ② If you call the discard() method with a value that doesn’t exist in the set, it does nothing. No error; it’s just a no-op.

- ④ Here’s the difference: if the value doesn’t exist in the set, the remove() method raises a KeyError exception.

- Like lists, sets have a pop() method.

```python
a_set = {1, 3, 6, 10, 15, 21, 28, 36, 45}
print (a_set.pop())                                #①
#1

print (a_set.pop())
#3

print (a_set.pop())
#36

print (a_set)
#{6, 10, 45, 15, 21, 28}

a_set.clear()                                      #②
print (a_set)
#set()

print (a_set.pop() )                               #③
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 18, in <module>
# print (a_set.pop() ) #\u2462
#KeyError: 'pop from an empty set'

```
</br>
- ① The pop() method removes a single value from a set and returns the value. However, since sets are unordered, there is no “last” value in a set, ***so there is no way to control which value gets removed. It is completely arbitrary.***
</br>
- ② The clear() method removes all values from a set, leaving you with an empty set. This is equivalent to a_set = set(), which would create a new empty set and overwrite the previous value of the a_set variable.

- ③ Attempting to pop a value from an empty set will raise a KeyError exception.
</br>
</br>
### - Common Set Operations :
</br>
Python’s set type supports several common set operations.

```python

a_set = {2, 4, 5, 9, 12, 21, 30, 51, 76, 127, 195}
print (30 in a_set)                                                     #①
#True

print (31 in a_set)
#False

b_set = {1, 2, 3, 5, 6, 8, 9, 12, 15, 17, 18, 21}
print (a_set.union(b_set))                                              #②
#{1, 2, 195, 4, 5, 6, 8, 12, 76, 15, 17, 18, 3, 21, 30, 51, 9, 127}

print (a_set.intersection(b_set))                                       #③
#{9, 2, 12, 5, 21}

print (a_set.difference(b_set) )                                        #④
#{195, 4, 76, 51, 30, 127}

print (a_set.symmetric_difference(b_set))                               #⑤
#{1, 3, 4, 6, 8, 76, 15, 17, 18, 195, 127, 30, 51}

```

</br>

-  ① To test whether a value is a member of a set, use the in operator. This works the same as lists.

-  ② The union() method returns a new set containing all the elements that are in either set.

-  ③ The intersection() method returns a new set containing all the elements that are in both sets.

-  ④ The difference() method returns a new set containing all the elements that are in a_set but not b_set.

-  ⑤ The symmetric_difference() method ***returns a new set containing all the elements that are in exactly one of the sets***.

Three of these methods are symmetric.
</br>

```python
# continued from the previous example
a_set = {2, 4, 5, 9, 12, 21, 30, 51, 76, 127, 195}
b_set = {1, 2, 3, 5, 6, 8, 9, 12, 15, 17, 18, 21}

print (b_set.symmetric_difference(a_set))                                       #①
#{1, 195, 4, 3, 6, 8, 76, 15, 17, 18, 51, 30, 127}

print (b_set.symmetric_difference(a_set) == a_set.symmetric_difference(b_set))  #②
#True

print (b_set.union(a_set) == a_set.union(b_set))                                #③
#True

print (b_set.intersection(a_set) == a_set.intersection(b_set) )                 #④
#True

print (b_set.difference(a_set) == a_set.difference(b_set) )                     #⑤
#False
```

</br>

-   ***① The symmetric difference of a_set from b_set looks different than the symmetric difference of b_set from a_set, but remember, sets are unordered.*** Any two sets that contain all the same values (with none left over) are considered equal.

-   ② And that’s exactly what happens here. Don’t be fooled by the Python Shell’s printed representation of these sets. They contain the same values, so they are equal.

-   ③ The union of two sets is also symmetric.

-   ④ The intersection of two sets is also symmetric.

-   ⑤ The difference of two sets is not symmetric. That makes sense; it’s analogous to subtracting one number from another. The order of the operands matters.
</br>
</br>

Finally, there are a few questions you can ask of sets.

```python
a_set = {1, 2, 3}
b_set = {1, 2, 3, 4}
print (a_set.issubset(b_set))    #①
#True

print (b_set.issuperset(a_set))  #②
#True

a_set.add(5)                     #③
print (a_set.issubset(b_set))
```

-   ① a_set is a subset of b_set — all the members of a_set are also members of b_set.

-   ② Asking the same question in reverse, b_set is a superset of a_set, because all the members of a_set are also members of b_set.

-   ③ As soon as you add a value to a_set that is not in b_set, both tests return False.
</br>
</br>
</br>

### - Sets In A Boolean Context :
</br>
You can use sets in a boolean context, such as an if statement.
</br>

```python
def is_it_true(anything):
   if anything:
     print("yes, it's true")
   else:
     print("no, it's false")

print (is_it_true(set()))          #①
#no, it's false
#None

print (is_it_true({'a'}))          #②
#yes, it's true
#None

print (is_it_true({False}))        #③
#yes, it's true
#None
```
</br>
</br>

-   ① In a boolean context, an empty set is false.

-   ② Any set with at least one item is true.

-   ③ Any set with at least one item is true. The value of the items is irrelevant.