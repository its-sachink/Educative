# List Comprehensions :

```python
a_list = [1, 9, 8, 4]
print ([elem * 2 for elem in a_list] )          #①
#[2, 18, 16, 8]

print (a_list)                                  #②
#[1, 9, 8, 4]

a_list = [elem * 2 for elem in a_list]          #③
print (a_list)
#[2, 18, 16, 8]
```
</br>
</br>
- You can use <mark>python expression in a list comprehension</mark>

```python
import os, glob
print (glob.glob('*.xml') )                                #①
#['feed.xml']

print ([os.path.realpath(f) for f in glob.glob('*.xml')])  #②
#['/usercode/feed.xml']
```

</br>
</br>

- List comprehensions can also filter items.
- This list comprehension looks at the list of all .py files in the current directory, and the <mark>if expression filters that list by testing whether the size of each file is smaller than 6000 bytes.</mark>
```python
import os, glob
print ([f for f in glob.glob('*.py') if os.stat(f).st_size < 6000])  #①
#['customserializer.py', 'romantest3.py', '__ed_file.py', 'romantest1.py', 
# 'humansize.py', 'pickleversion.py', 'plural6.py', 'stdout.py', 
# 'fibonacci2.py', 'roman8.py', 'alphametics.py', 'roman3.py', 'oneline.py', 
#'roman1.py', 'roman2.py', 'roman10.py', 'roman9.py', 'romantest2.py']
```

</br>
</br>

```python
import os, glob
print ([(os.stat(f).st_size, os.path.realpath(f)) for f in glob.glob('*.xml')] )           #①
#[(2796, '/usercode/feed.xml')]

import humansize
print ([(humansize.approximate_size(os.stat(f).st_size), f) for f in glob.glob('*.xml')])  #②
#[('2.7 KiB', 'feed.xml')]
```

- ① This list comprehension finds all the .xml files in the current working directory, gets the size of each file (by calling the os.stat() function), and constructs a tuple of the file size and the absolute path of each file (by calling the os.path.realpath() function).
- ② <mark>This comprehension builds on the previous one to call the approximate_size() function with the file size of each .xml file.</mark>
