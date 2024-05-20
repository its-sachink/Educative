# Calculating Permutations… The Lazy Way!

- The idea is that you take a list of things (could be numbers, could be letters, could be dancing bears) and find all the possible ways to split them up into smaller lists. All the smaller lists have the same size, which can be as small as 1 and as large as the total number of items. Oh, and nothing can be repeated.
- “let’s find the permutations of 3 different items taken 2 at a time,” which means you have a sequence of 3 items and you want to find all the possible ordered pairs.

```python
import itertools                             #①
perms = itertools.permutations([1, 2, 3], 2) #②
print (next(perms))                          #③
#(1, 2)

print (next(perms))
#(1, 3)

print (next(perms))
#(2, 1)                                      #④

print (next(perms))
#(2, 3)

print (next(perms))
#(3, 1)

print (next(perms))
#(3, 2)

print (next(perms))                                   #⑤
#Traceback (most recent call last):
#  File "/usercode/__ed_file.py", line 21, in <module>
# print (next(perms)) #\u2464
#StopIteration
```

- ① The itertools module has all kinds of fun stuff in it, including a permutations() function that does all the hard work of finding permutations.
- ② The permutations() function takes a sequence (here a list of three integers) and a number, which is the number of items you want in each smaller group. The function returns an iterator, which you can use in a for loop or any old place that iterates.
- ③ The first permutation of [1, 2, 3] taken 2 at a time is (1, 2).
- When there are no more permutations, the iterator raises a StopIteration exception.


- The permutations() function doesn’t have to take a list. It can take any sequence — even a string.
```python
import itertools
perms = itertools.permutations('ABC', 3)  #①
print (next(perms))
#('A', 'B', 'C')                          #②

print (next(perms))
#('A', 'C', 'B')

print (next(perms))
#('B', 'A', 'C')

print (next(perms))
#('B', 'C', 'A')

print (next(perms))
#('C', 'A', 'B')

print (next(perms))
#('C', 'B', 'A')

print (next(perms))
#Traceback (most recent call last):
#  File "/usercode/__ed_file.py", line 21, in <module>
# print (next(perms))
#StopIteration
```

- You can also pass it to the Lists functions.

```python
import itertools
perms = itertools.permutations('ABC', 3)          

print (list(itertools.permutations('ABC', 3)) )   #③
#[('A', 'B', 'C'), ('A', 'C', 'B'),
# ('B', 'A', 'C'), ('B', 'C', 'A'),
# ('C', 'A', 'B'), ('C', 'B', 'A')]
```

