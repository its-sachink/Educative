# Formatting Strings :

</br></br>
```python
SUFFIXES = {1000: ['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'],         #①
            1024: ['KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']}

def approximate_size(size, a_kilobyte_is_1024_bytes=True):
    '''Convert a file size to human-readable form.                          #②

    Keyword arguments:
    size -- file size in bytes
    a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024
                                if False, use multiples of 1000

    Returns: string

    '''                                                                     #③
    if size < 0:
        raise ValueError('number must be non-negative')                     #④

    multiple = 1024 if a_kilobyte_is_1024_bytes else 1000
    for suffix in SUFFIXES[multiple]:
        size /= multiple
        if size < multiple:
            return '{0:.1f} {1}'.format(size, suffix)                       #⑤

    raise ValueError('number too large')
    
```
</br>
- ① 'KB', 'MB', 'GB'… those are each strings.
- ② Function docstrings are strings.
- ④ There’s another string, being passed to the exception as a human-readable error message.

</br>
- Python 3 supports formatting values into strings. Although this can include very complicated expressions, the most basic usage is to insert a value into a string with a single placeholder.
</br>

```python
username = 'mark'
password = 'PapayaWhip'                                     #①
print ("{0}'s password is {1}".format(username, password))  #②
#"mark's password is PapayaWhip"
```

</br>
</br>
## Compound field names :
</br>
- The previous example shows the simplest case, where the replacement fields are simply integers. Integer replacement fields are treated as positional indices into the argument list of the format() method. That means that {0} is replaced by the first argument (username in this case), {1} is replaced by the second argument (password), &c.
</br>
```python
import humansize
si_suffixes = humansize.SUFFIXES[1000]              #①
print (si_suffixes)
#['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB']

print ('1000{0[0]} = 1{0[1]}'.format(si_suffixes))  #②
#'1000KB = 1MB'
```

</br>
- So {0[0]} refers to the first item of the list which is the first argument passed to the format() method: 'KB'. Meanwhile, {0[1]} refers to the second item of the same list: 'MB'. Everything outside the curly braces — including 1000, the equals sign, and the spaces — is untouched. The final result is the string '1000KB = 1MB'.
</br>
-  The following compound field names “just work”:
    - Passing a list, and accessing an item of the list by index (as in the previous example)
    - Passing a dictionary, and accessing a value of the dictionary by key
    - Passing a module, and accessing its variables and functions by name
    - Passing a class instance, and accessing its properties and methods by name
    - Any combination of the above
</br>

```python
import humansize
import sys
print ('1MB = 1000{0.modules[humansize].SUFFIXES[1000][0]}'.format(sys))
#1MB = 1000KB
```
</br>
- The sys module holds information about the currently running Python instance. Since you just imported it, you can pass the sys module itself as an argument to the format() method. So the replacement field {0} refers to the sys module.
- <mark>sys.modules is a dictionary of all the modules that have been imported in this Python instance.</mark> The keys are the module names as strings; the values are the module objects themselves. <mark>So the replacement field {0.modules} refers to the dictionary of imported modules.</mark>
</br>

    - sys.modules['humansize'].SUFFIXES is the dictionary defined at the top of the humansize module. The replacement field {0.modules[humansize].SUFFIXES} refers to that dictionary.
</br>
    - sys.modules['humansize'].SUFFIXES[1000] is a list of SI suffixes: ['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB']. So the replacement field {0.modules[humansize].SUFFIXES[1000]} refers to that list.
</br>
    - <mark>sys.modules['humansize'].SUFFIXES[1000][0] is the first item of the list of SI suffixes: 'KB'. Therefore, the complete replacement field {0.modules[humansize].SUFFIXES[1000][0]} is replaced by the two-character string KB.</mark>
    </br>



- <mark>The format specifier “.1” means “round to the nearest tenth” (i.e. display only one digit after the decimal point). The format specifier “f” means “fixed-point number” (as opposed to exponential notation or some other decimal representation).</mark>

```python
print ('{0:.1f} {1}'.format(698.24, 'GB'))
#698.2 GB
```
