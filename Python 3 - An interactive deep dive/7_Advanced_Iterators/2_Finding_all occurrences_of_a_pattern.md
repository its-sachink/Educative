# Finding all occurrences of a pattern

</br>
</br>

- The first thing this alphametics solver does is find all the letters (A–Z) in the puzzle.

```python
import re
print (re.findall('[0-9]+', '16 2-by-4s in rows of 8'))  #①
#['16', '2', '4', '8']
print (re.findall('[A-Z]+', 'SEND + MORE == MONEY'))     #②
#['SEND', 'MORE', 'MONEY']
```
</br>

- ① The re module is Python’s implementation of regular expressions. It has a nifty function called findall() which takes a regular expression pattern and a string, and finds all occurrences of the pattern within the string.

- Below the regular expression looks for a space, an s, and then the shortest possible series of any character (.*?), then a space, then another s.

```python
import re
print (re.findall(' s.*? s', "The sixth sick sheikh's sixth sheep's sick."))
#[' sixth s', " sheikh's s", " sheep's s"]
```
- output
```
Output
0.82s
[' sixth s', " sheikh's s", " sheep's s"]
```

