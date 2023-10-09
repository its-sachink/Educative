# Other Common String Methods

</br>
</br>

```python
s = '''Finished files are the re-  
 sult of years of scientif-
 ic study combined with the
 experience of years.'''
                                    #①
print(s.splitlines())               #②
#['Finished files are the re-',
# 'sult of years of scientif-',
# 'ic study combined with the',
# 'experience of years.']

print(s.lower())                    #③
#finished files are the re-
#sult of years of scientif-
#ic study combined with the
#experience of years.

print(s.lower().count('f'))         #④
#6
```
</br>

```console
['Finished files are the re-  ', ' sult of years of scientif-', ' ic study combined with the', ' experience of years.']
finished files are the re-  
 sult of years of scientif-
 ic study combined with the
 experience of years.
6
```

</br>
</br>
Let’s say you have a list of key-value pairs in the form key1=value1&key2=value2, and you want to split them up and make a dictionary of the form {key1: value1, key2: value2}.
</br>

```python
query = 'user=pilgrim&database=master&password=PapayaWhip'
a_list = query.split('&')                                        #①
print (a_list)
#['user=pilgrim', 'database=master', 'password=PapayaWhip']

a_list_of_lists = [v.split('=', 1) for v in a_list if '=' in v]  #②
print (a_list_of_lists)
#[['user', 'pilgrim'], ['database', 'master'], ['password', 'PapayaWhip']]

a_dict = dict(a_list_of_lists)                                   #③
print (a_dict)
#{'user': 'pilgrim', 'database': 'master', 'password': 'PapayaWhip'}
```

- ① The split() string method has one required argument, a delimiter. The method splits a string into a list of strings based on the delimiter. Here, the delimiter is an ampersand character, but it could be anything.
- ② The optional second argument to the split() method is the number of times you want to split. 1 means “only split once,” so the split() method will return a two-item list. (In theory, a value could contain an equals sign too. If you just used 'key=value=foo'.split('='), you would end up with a three-item list ['key', 'value', 'foo'].)
- ③ Finally, Python can turn that list-of-lists into a dictionary simply by passing it to the dict() function.

</br>
</br>
## Slicing A String :
</br>
- Once you’ve defined a string, you can get any part of it as a new string. This is called slicing the string. 
    - Slicing strings works exactly the same as slicing lists, which makes sense, because strings are just sequences of characters.

    ```python
    a_string = 'My alphabet starts where your alphabet ends.'
print (a_string[3:11])           #①
#alphabet

print (a_string[3:-3])           #②
#alphabet starts where your alphabet en

print (a_string[0:2] )           #③
#My

print (a_string[:18])            #④
#My alphabet starts

print (a_string[18:] )           #⑤
# where your alphabet ends.
    ```
</br>
- ③ Strings are zero-based, so a_string[0:2] returns the first two items of the string, starting at a_string[0], up to but not including a_string[2].
- ④ If the left slice index is 0, you can leave it out, and 0 is implied. So a_string[:18] is the same as a_string[0:18], because the starting 0 is implied.
- ⑤ Similarly, if the right slice index is the length of the string, you can leave it out. So a_string[18:] is the same as a_string[18:44], because this string has 44 characters.

