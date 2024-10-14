# Verbose Regular Expressions

- Regular expressions are difficult to read, and even if you figure out what one does, that’s no guarantee that you’ll be able to understand it six months later. What you really need is inline documentation.
- Python allows you to do this with something called verbose regular expressions. verbose regular expression is different from a compact regular expression in two ways:
    - <mark>Whitespace is ignored. Spaces, tabs, and carriage returns are not matched as spaces, tabs, and carriage returns. They’re not matched at all.</mark> (If you want to match a space in a verbose regular expression, you’ll need to escape it by putting a backslash in front of it.)
    - <mark>Comments are ignored.</mark> A comment in a verbose regular expression is just like a comment in Python code: it starts with a # character and goes until the end of the line.

```python
import re
pattern = '''
    ^                   # beginning of string
    M{0,3}              # thousands - 0 to 3 Ms
    (CM|CD|D?C{0,3})    # hundreds - 900 (CM), 400 (CD), 0-300 (0 to 3 Cs),
                        #            or 500-800 (D, followed by 0 to 3 Cs)
    (XC|XL|L?X{0,3})    # tens - 90 (XC), 40 (XL), 0-30 (0 to 3 Xs),
                        #        or 50-80 (L, followed by 0 to 3 Xs)
    (IX|IV|V?I{0,3})    # ones - 9 (IX), 4 (IV), 0-3 (0 to 3 Is),
                        #        or 5-8 (V, followed by 0 to 3 Is)
    $                   # end of string
    '''

print (re.search(pattern, 'M', re.VERBOSE))                 #①
#<_sre.SRE_Match object at 0x008EEB48>

print (re.search(pattern, 'MCMLXXXIX', re.VERBOSE))         #②
#<_sre.SRE_Match object at 0x008EEB48>

print (re.search(pattern, 'MMMDCCCLXXXVIII', re.VERBOSE))   #③
#<_sre.SRE_Match object at 0x008EEB48>

print (re.search(pattern, 'M') )                            #④
```

</br>

```console
<_sre.SRE_Match object; span=(0, 1), match='M'>
<_sre.SRE_Match object; span=(0, 9), match='MCMLXXXIX'>
<_sre.SRE_Match object; span=(0, 15), match='MMMDCCCLXXXVIII'>
None
```
</br>
</br>
</br>
-  ① The most important thing to remember when using verbose regular expressions is that you need to pass an extra argument when working with them: ** re.VERBOSE ** is a constant defined in the re module that signals that the pattern should be treated as a verbose regular expression.
