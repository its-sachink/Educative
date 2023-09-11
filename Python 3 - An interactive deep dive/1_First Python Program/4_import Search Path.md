# The 'import' Search Path

Python looks in several places when you try to import a module. Specifically, it looks in all the directories defined in sys.path. This is just a list, and you can easily view it or modify it with standard list methods. (You’ll learn more about lists in Native Datatypes.)

```python
import sys                                                         #①

print (sys.path)                                                   #②
#['/usercode', 
# '/usr/lib/python3.4', 
# '/usr/lib/python3.4/plat-x86_64-linux-gnu', 
# '/usr/lib/python3.4/lib-dynload', 
# '/usr/local/lib/python3.4/dist-packages', 
# '/usr/lib/python3/dist-packages']

print (sys)                                                        #③
#<module 'sys' (built-in)>

print (sys.path.insert(0, '/home/mark/diveintopython3/examples'))  #④
#None

print (sys.path)                                                   #⑤
#['/home/mark/diveintopython3/examples', 
#'/usercode', 
#'/usr/lib/python3.4', 
#'/usr/lib/python3.4/plat-x86_64-linux-gnu', 
#'/usr/lib/python3.4/lib-dynload', 
#'/usr/local/lib/python3.4/dist-packages', 
#'/usr/lib/python3/dist-packages']
```

- ① Importing the 'sys' module makes all of its functions and attributes available.
</br>
- ② sys.path is a list of directory names that constitute the current search path. Python will look through these directories (in this order) for a .py file whose name matches what you’re trying to import.
</br>
- ③ Not all modules are stored as .py files. Some are built-in modules; they are actually baked right into Python itself. Built-in modules behave just like regular modules, but their Python source code is not available, because they are not written in Python! (Like Python itself, these built-in modules are written in C.)
</br>
- ④ You can add a new directory to Python’s search path at runtime by adding the directory name to 'sys.path'
</br>
- ⑤ By using sys.path.insert(0, new_path), you inserted a new directory as the first item of the sys.path list