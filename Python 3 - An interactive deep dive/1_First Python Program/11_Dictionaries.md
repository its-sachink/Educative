# Dictionaries :
</br>
</br>

-   A dictionary is an unordered set of key-value pairs. When you add a key to a dictionary, you must also add a value for that key.
-   Python dictionaries are optimized for retrieving the value when you know the key, but not the other way around.
</br>

### Creating a dictionary :
</br>

```python
a_dict = {'server': 'db.diveintopython3.org', 'database': 'mysql'}          #①
print (a_dict)
#{'server': 'db.diveintopython3.org', 'database': 'mysql'}

print (a_dict['server'] )                                                   #②
#db.diveintopython3.org

print (a_dict['database'] )                                                 #③
#mysql

print (a_dict['db.diveintopython3.org'])                                    #④
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 11, in <module>
# print (a_dict['db.diveintopython3.org']) #\u2463
#KeyError: 'db.diveintopython3.org'
```
-   ④ You can get values by key, but you can’t get keys by value. So a_dict['server'] is 'db.diveintopython3.org', but a_dict['db.diveintopython3.org'] raises an exception, because 'db.diveintopython3.org' is not a key.

</br>
</br>
### Modifying a dictionary :
</br>

```python
a_dict = {'server': 'db.diveintopython3.org', 'database': 'mysql'}
print (a_dict)
#{'server': 'db.diveintopython3.org', 'database': 'mysql'}

a_dict['database'] = 'blog'  #①
print (a_dict)
#{'server': 'db.diveintopython3.org', 'database': 'blog'}

a_dict['user'] = 'mark'      #②
print (a_dict )              #③
#{'server': 'db.diveintopython3.org', 'database': 'blog', 'user': 'mark'}

a_dict['user'] = 'dora'      #④
print (a_dict)
#{'server': 'db.diveintopython3.org', 'database': 'blog', 'user': 'dora'}

a_dict['User'] = 'mark'      #⑤
print (a_dict)
#{'server': 'db.diveintopython3.org', 'User': 'mark', 'database': 'blog', 'user': 'dora'}
```

-   ⑤ Will this change the value of the user key back to “mark”? No! Look at the key closely — that’s a capital U in "User".
-   ***Dictionary keys are case-sensitive***, so this statement is creating a new key-value pair, not overwriting an existing one. It may look similar to you, but as far as Python is concerned, it’s completely different.
</br>
</br>

### Mixed-value dictionaries :
</br>
</br>

-   Dictionaries aren’t just for strings. Dictionary values can be any datatype, including integers, booleans, arbitrary objects, or even other dictionaries.

```python
SUFFIXES = {1000: ['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'],
             1024: ['KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']}

print (len(SUFFIXES))      #①
#2

print (1000 in SUFFIXES)   #②
#True

print (SUFFIXES[1000] )    #③
#['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB']

print (SUFFIXES[1024])     #④
#['KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']

print (SUFFIXES[1000][3])  #⑤
#'TB'
```
-   ① Like lists and sets, the len() function gives you the number of keys in a dictionary.

</br>
</br>

### Dictionaries in a boolean context :

```python
def is_it_true(anything):
   if anything:
     print("yes, it's true")
   else:
     print("no, it's false")

print (is_it_true({}) )            #①
#no, it's false
#None
print (is_it_true({'a': 1}))       #②
#yes, it's true
#None
```

- ① In a boolean context, an empty dictionary is false.

- ② Any dictionary with at least one key-value pair is true.

