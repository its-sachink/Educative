# Use Regular Expressions! :
</br>

## Regular expression substitutions example :

```python
import re
print (re.search('[abc]', 'Mark'))    #①
#<_sre.SRE_Match object at 0x001C1FA8>

print (re.sub('[abc]', 'o', 'Mark'))  #②
#Mork

print (re.sub('[abc]', 'o', 'rock'))  #③
#rook

print (re.sub('[abc]', 'o', 'caps'))  #④
#oops
```
</br>

- ① Check if the string Mark contain a, b, or c? Yes, it contains a.
- ② Find a, b, or c, and replace it with o. Mark becomes Mork.
- ③ same function turns rock into rook.
- ④ re.sub replaces all of the matches, not just the first one. So this regular expression turns caps into oops, because both the c and the a get turned into o.
</br>
</br>


## Solution for our previous usecase of defining plurals :
</br>

- You have rules that say you need to find different combinations of characters, then do different things to them. This sounds like a job for regular expressions!

```python
import re

def plural(noun):          
    if re.search('[sxz]$', noun):            
        return re.sub('$', 'es', noun)         #①
    elif re.search('[^aeioudgkprt]h$', noun):  #②
        return re.sub('$', 'es', noun)
    elif re.search('[^aeiou]y$', noun):        #③
        return re.sub('y$', 'ies', noun)     
    else:
        return noun + 's'
```
</br>

- ① quare brackets mean “match exactly one of these characters.” So [sxz] means “s, or x, or z”, but only one of them.
    - ＄ should be familiar; it matches the end of string.
    - Combined, this regular expression tests whether noun ends with s, x, or z.
    - you’re replacing the end of the string (matched by ＄) with the string es.
- ② The ^ as the first character inside the square brackets means : negation. [^abc] means “any single character except a, b, or c”.
    - So [^aeioudgkprt] means any character **except** a, e, i, o, u, d, g, k, p, r, or t. Then that character needs to be followed by h, followed by end of string.
- ③ where the character before the Y is not a, e, i, o, or u. You’re looking for words that end in Y that sounds like I.

</br>
</br>


## Another look at negation regular expression :
</br>

```python
import re
print (re.search('[^aeiou]y$', 'vacancy'))  #①
#<_sre.SRE_Match object at 0x001C1FA8>

print (re.search('[^aeiou]y$', 'boy'))      #②
#None

print (re.search('[^aeiou]y$', 'day'))
#None

print (re.search('[^aeiou]y$', 'pita'))     #③
#None
```
```console
<_sre.SRE_Match object; span=(5, 7), match='cy'>
None
None
None
```
</br>

- ① vacancy matches this regular expression, because it ends in cy, and c is not a, e, i, o, or u.
- ② boy does not match, because it ends in oy.
    - **you specifically said that the character before the y could not be o**.
    - day does not match, because it ends in ay.
- ③ pita does not match, because it does not end in y.
</br>
</br>


## One more look at re.sub() :

```python
import re
print (re.sub('y$', 'ies', 'vacancy') )              #①
#vacancies

print (re.sub('y$', 'ies', 'agency'))
#agencies

print (re.sub('([^aeiou])y$', r'\1ies', 'vacancy'))  #②
#vacancies
```

```console
vacancies
agencies
vacancies
```

- ② you use a new syntax, \1, which means “hey, that first group you remembered? put it right here.” In this case, you remember the c before the y; when you do the substitution, you substitute c in place of c, and ies in place of y. (If you have more than one remembered group, you can use \2 and \3 and so on.)