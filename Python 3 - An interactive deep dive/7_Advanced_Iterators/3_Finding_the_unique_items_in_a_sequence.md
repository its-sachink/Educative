# Finding the unique items in a sequence :

```python
a_list = ['The', 'sixth', 'sick', "sheik's", 'sixth', "sheep's", 'sick']
print (set(a_list) )                                #①
#{'sixth', 'The', "sheep's", 'sick', "sheik's"}

a_string = 'EAST IS EAST'
print (set(a_string) )                              #②
#{'A', 'E', 'S', ' ', 'T', 'I'}

words = ['SEND', 'MORE', 'MONEY']
print (''.join(words))                              #③
#SENDMOREMONEY

print (set(''.join(words))  )                       #④
#{'R', 'M', 'E', 'S', 'Y', 'O', 'N', 'D'}
```

- The alphametics solver uses this technique to build a set of all the unique characters in the puzzle.

```
unique_characters = set(''.join(words))
```
