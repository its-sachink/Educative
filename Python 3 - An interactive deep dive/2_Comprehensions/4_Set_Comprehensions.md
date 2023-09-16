# Set Comprehensions :
</br>
</br>
-   Syntax is remarkably similar to the syntax for dictionary comprehensions. The only difference is that sets just have values instead of key:value pairs.

```python
a_set = set(range(10))
print (a_set)
#{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}

print ({x ** 2 for x in a_set} )          #①
#{0, 1, 64, 4, 36, 9, 16, 49, 81, 25}

print ({x for x in a_set if x % 2 == 0})  #②
#{0, 8, 2, 4, 6}

print ({2**x for x in range(10)})         #③
#{32, 1, 2, 64, 4, 128, 256, 512, 8, 16}
```
</br>

-   ① Set comprehensions can take a set as input. This set comprehension calculates the squares of the set of numbers from 0 to 9.
-   ③ Set comprehensions do not need to take a set as input; they can take any sequence.