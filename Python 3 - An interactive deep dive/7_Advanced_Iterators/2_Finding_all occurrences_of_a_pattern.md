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
