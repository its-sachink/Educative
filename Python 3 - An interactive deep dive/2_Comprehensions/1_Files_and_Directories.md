# Working with files and directories :
</br>
</br>
-   The os module contains two functions to deal with the current working directory.
</br>

```python
import os, sys                                        #①
os.getcwd()                                           #②
#/C:\Python31

os.chdir('/Users/pilgrim/diveintopython3/examples')   #③
os.getcwd()                                           #④
#C:\Users\pilgrim\diveintopython3\examples
```
</br>
-   ④ When I called the os.chdir() function, I used a Linux-style pathname (forward slashes, no drive letter) even though I’m on Windows. This is one of the places where Python tries to paper over the differences between operating systems.
</br>
</br>

## Working with filenames and directory names :
</br>

```python
import os
print(os.path.join('/Users/pilgrim/diveintopython3/examples/', 'humansize.py'))              #①
#/Users/pilgrim/diveintopython3/examples/humansize.py

print(os.path.join('/Users/pilgrim/diveintopython3/examples', 'humansize.py'))               #②
#/Users/pilgrim/diveintopython3/examples\humansize.py

print(os.path.expanduser('~'))                                                               #③
#/nonexistent

print(os.path.join(os.path.expanduser('~'), 'diveintopython3', 'examples', 'humansize.py'))  #④
#/nonexistent/diveintopython3/examples/humansize.py
```

-   ② In this slightly less trivial case, calling the os.path.join() function will add an extra slash to the pathname before joining it to the filename. It’s a backslash instead of a forward slash, because I constructed this example on Windows. If you replicate this example on Linux or Mac OS X, you’ll see a forward slash instead. Don’t fuss with slashes; always use os.path.join() and let Python do the right thing.
-   ④ Combining these techniques, you can easily construct pathnames for directories and files in the user’s home directory. The os.path.join() function can take any number of arguments. I was overjoyed when I discovered this, since addSlashIfNecessary() is one of the stupid little functions I always need to write when building up my toolbox in a new language. Do not write this stupid little function in Python; smart people have already taken care of it for you.

</br>
</br>
-   os.path also contains functions to split full pathnames, directory names, and filenames into their constituent parts.
</br>

```python
import os
pathname = '/Users/pilgrim/diveintopython3/examples/humansize.py'
print (os.path.split(pathname) )                                       #①
#('/Users/pilgrim/diveintopython3/examples', 'humansize.py')

(dirname, filename) = os.path.split(pathname)                          #②
print (dirname )                                                       #③
#/Users/pilgrim/diveintopython3/examples

print (filename )                                                      #④
#humansize.py

(shortname, extension) = os.path.splitext(filename)                    #⑤
print (shortname)
#humansize

print (extension)
#.py
```
-   ⑤ os.path also contains the os.path.splitext() function, which splits a filename and returns a tuple containing the filename and the file extension. You use the same technique to assign each of them to separate variables.

</br>
</br>

## Listing directories :
</br>
-   The glob module is another tool in the Python standard library. It’s an easy way to get the contents of a directory programmatically, and it uses the sort of wildcards that you may already be familiar with from working on the command line.
</br>

```python
import os
os.chdir('/Users/pilgrim/diveintopython3/')
import glob

glob.glob('examples/*.xml')                  #①
#['examples\\feed-broken.xml',
# 'examples\\feed-ns0.xml',
# 'examples\\feed.xml']

os.chdir('examples/')                        #②
glob.glob('*test*.py')                       #③
#['alphameticstest.py',
# 'pluraltest1.py',
# 'pluraltest2.py',
# 'pluraltest3.py',
# 'pluraltest4.py',
# 'pluraltest5.py',
# 'pluraltest6.py',
# 'romantest1.py',
# 'romantest10.py',
# 'romantest2.py',
# 'romantest3.py',
# 'romantest4.py',
# 'romantest5.py',
# 'romantest6.py',
# 'romantest7.py',
# 'romantest8.py',
# 'romantest9.py']
```

-   ③ You can include multiple wildcards in your glob pattern. This example finds all the files in the current working directory that end in a .py extension and contain the word test anywhere in their filename.

</br>

## Getting file metadata :
</br>
- Every modern file system stores metadata about each file: creation date, last-modified date, file size, and so on.
</br>

```python
import os
print(os.getcwd())                         #①
#/usercode

metadata = os.stat('feed.xml')             #②
print (metadata.st_mtime)                  #③
#1317786276.0

import time                                #④
print (time.localtime(metadata.st_mtime))  #⑤
#time.struct_time(tm_year=2011, tm_mon=10, 
# tm_mday=5, tm_hour=3, tm_min=44, tm_sec=36, tm_wday=2, tm_yday=278, tm_isdst=0)
```

-   ③ st_mtime is the modification time, but it’s in a format that isn’t terribly useful. (Technically, it’s the number of seconds since the Epoch, which is defined as the first second of January 1st, 1970. Seriously.)
-   ⑤ The time.localtime() function converts a time value from seconds-since-the-Epoch (from the st_mtime property returned from the os.stat() function) into a more useful structure of year, month, day, hour, minute, second, and so on. This file was last modified on July 13, 2009, at around 5:25 PM.

```python
# continued from the previous example

metadata.st_size                              #①
#3070

import humansize
humansize.approximate_size(metadata.st_size)  #②
#'3.0 KiB'
```

</br>
</br>

## Constructing absolute pathnames :
</br>
-   the glob.glob() function returned a list of relative pathnames.
-   But if you want to construct an absolute pathname — i.e. one that includes all the directory names back to the root directory or drive letter — then you’ll need the os.path.realpath() function.

```python
import os
print(os.getcwd())
#/usercode

print(os.path.realpath('feed.xml'))
#/usercode/feed.xml
```


