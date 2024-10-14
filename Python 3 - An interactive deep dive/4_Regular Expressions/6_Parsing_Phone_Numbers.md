# Parsing Phone Numbers :

- Here are the phone numbers I needed to be able to accept:

    - 800-555-1212
    - 800 555 1212
    - 800.555.1212
    - (800) 555-1212
    - 1-800-555-1212
    - 800-555-1212-1234
    - 800-555-1212x1234
    - 800-555-1212 ext. 1234
    - work 1-(800) 555.1212 #1234

</br>
</br>

## Solution 1 :

```python
import re
phonePattern = re.compile(r'^(\d{3})-(\d{3})-(\d{4})$')          #①
print (phonePattern.search('800-555-1212').groups())             #②
#('800', '555', '1212')

print (phonePattern.search('800-555-1212-1234'))                 #③
#None

print (phonePattern.search('800-555-1212-1234').groups())        #④
#Traceback (most recent call last):
# File "/usercode/__ed_file.py", line 8, in <module>
# print (phonePattern.search('800-555-1212-1234').groups()) #\u2463
#AttributeError: 'NoneType' object has no attribute 'groups'
```
</br>

- ① What’s \d{3}? Well, <mark>\d means “any numeric digit” (0 through 9). The {3} means “match exactly three numeric digits”; it’s a variation on the {n,m} syntax you saw earlier.</mark>
    - all in <mark>parentheses means “match exactly three numeric digits, and then remember them as a **group** that I can ask for later”. Then match a literal hyphen.</mark>
    - Then match another group of exactly three digits. Then another literal hyphen. Then another group of exactly four digits. Then match the end of the string.

- ② To get access to the groups that the regular expression parser remembered along the way, use the groups() method on the object that the search() method returns.
    - you defined three groups, one with three digits, one with three digits, and one with four digits.

- ④ it returns None, not a regular expression match object. Calling None.groups() raises a perfectly obvious exception.


</br>
</br>

## Solution 2 :

```python
import re
phonePattern = re.compile(r'^(\d{3})-(\d{3})-(\d{4})-(\d+)$')  #①
print (phonePattern.search('800-555-1212-1234').groups())      #②
#('800', '555', '1212', '1234')

print (phonePattern.search('800 555 1212 1234') )              #③
#None

print (phonePattern.search('800-555-1212') )                   #④ 
#None
```
</br>

- ① What’s new is that you then match another hyphen, and a remembered group of one or more digits, then the end of the string.
- ② <mark>The groups() method now returns a tuple of four elements.</mark>



</br>
</br>

## Solution 3 :

```python
import re
phonePattern = re.compile(r'^(\d{3})\D+(\d{3})\D+(\d{4})\D+(\d+)$')  #①
print (phonePattern.search('800 555 1212 1234').groups() )           #②
#('800', '555', '1212', '1234')

print (phonePattern.search('800-555-1212-1234').groups())            #③
#('800', '555', '1212', '1234')

print (phonePattern.search('80055512121234'))                        #④
#None 
print (phonePattern.search('800-555-1212') )                         #⑤
#None
```
</br>

- ① <mark>\D+ : Well, \D matches any character except a numeric digit, and + means “1 or more”. So \D+ matches one or more characters that are not digits.</mark>


</br>
</br>

## Solution 4 :
```python
import re
phonePattern = re.compile(r'^(\d{3})\D*(\d{3})\D*(\d{4})\D*(\d*)$')   #①
print (phonePattern.search('80055512121234').groups())                #②
#('800', '555', '1212', '1234')

print (phonePattern.search('800.555.1212 x1234').groups())            #③
#('800', '555', '1212', '1234')

print (phonePattern.search('800-555-1212').groups())                  #④
#('800', '555', '1212', '')

print (phonePattern.search('(800)5551212 x1234'))                     #⑤ 
#None
```
</br>

- ① Instead of \D+ between the parts of the phone number, <mark>you now match on \D*. Remember that + means “1 or more”? Well, *means “zero or more”.</mark>
    - So now you should be able to parse phone numbers even when there is no separator character at all.
- ⑤ There’s an extra character before the area code, but the regular expression assumes that the area code is the first thing at the beginning of the string.

</br>
</br>

## Solution 5 :
```python
import re
phonePattern = re.compile(r'^\D*(\d{3})\D*(\d{3})\D*(\d{4})\D*(\d*)$')          #①
print (phonePattern.search('(800)5551212 ext. 1234').groups())                  #②
#('800', '555', '1212', '1234')

print (phonePattern.search('800-555-1212').groups())                            #③
#('800', '555', '1212', '')

print (phonePattern.search('work 1-(800) 555.1212 #1234'))                      #④ 
#None
```
</br>

- ① now you’re matching \D*, zero or more non-numeric characters, before the first remembered group (the area code). Notice that you’re not remembering these non-numeric characters (they’re not in parentheses).
- ② You can successfully parse the phone number, even with the leading left parenthesis before the area code.
- ④ Because there’s a 1 before the area code, but you assumed that all the leading characters before the area code were non-numeric characters (\D*).

</br>
</br>

## Solution 6 :
```python
import re
phonePattern = re.compile(r'(\d{3})\D*(\d{3})\D*(\d{4})\D*(\d*)$')         #①
print (phonePattern.search('work 1-(800) 555.1212 #1234').groups())        #②
#('800', '555', '1212', '1234')

print (phonePattern.search('800-555-1212').groups())                       #③
#('800', '555', '1212', '')

print (phonePattern.search('80055512121234').groups())                     #④
#('800', '555', '1212', '1234')
```
</br>

- ① <mark>Note the lack of ^ in this regular expression. You are not matching the beginning of the string anymore.</mark> There’s nothing that says you need to match the entire input with your regular expression.
    - The regular expression engine will do the hard work of figuring out where the input string starts to match, and go from there.
    - When a regular expression does match, you can pick out specific pieces of it. You can find out what matched where.
- ② Now you can successfully parse a phone number that includes leading characters and a leading digit, plus any number of any kind of separators around each part of the phone number.


</br>
</br>

## Solution 7 :
</br>
let’s write it out as a verbose regular expression, before you forget why you made the choices you made.
</br>

```python
import re
phonePattern = re.compile(r'''
                # don't match beginning of string, number can start anywhere
    (\d{3})     # area code is 3 digits (e.g. '800')
    \D*         # optional separator is any number of non-digits
    (\d{3})     # trunk is 3 digits (e.g. '555')
    \D*         # optional separator
    (\d{4})     # rest of number is 4 digits (e.g. '1212')
    \D*         # optional separator
    (\d*)       # extension is optional and can be any number of digits
    $           # end of string
    ''', re.VERBOSE)

print (phonePattern.search('work 1-(800) 555.1212 #1234').groups())  #①
#('800', '555', '1212', '1234')

print (phonePattern.search('800-555-1212'))                          #②
#('800', '555', '1212', '')
```
