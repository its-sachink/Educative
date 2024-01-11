# Generators :
</br>
</br>

## look at an interactive example first :

```python
def make_counter(x):
     print('entering make_counter')
     while True:
         yield x                           #①
         print('incrementing x')
         x = x + 1
 

counter = make_counter(2)                  #②
print (counter)                            #③
#<generator object at 0x001C9C10>

print (next(counter))                      #④
#entering make_counter
#2

print (next(counter))                      #⑤
#incrementing x
#3

print (next(counter))                      #⑥
#incrementing x
#4
```

