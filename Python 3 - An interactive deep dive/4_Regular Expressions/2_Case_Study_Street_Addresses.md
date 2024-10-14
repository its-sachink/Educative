# Case Study: Street Addresses

```python
s = '100 NORTH MAIN ROAD'
print(s.replace('ROAD', 'RD.'))               #①
#'100 NORTH MAIN RD.'

s = '100 NORTH BROAD ROAD'
print(s.replace('ROAD', 'RD.'))               #②
#'100 NORTH BRD. RD.'

print(s[:-4] + s[-4:].replace('ROAD', 'RD.')) #③
#'100 NORTH BROAD RD.'

import re                                     #④
print(re.sub('ROAD$', 'RD.', s))              #⑤
#'100 NORTH BROAD RD.'
```
</br>
- Below is the console output. My goal is to standardize a street address so that 'ROAD' is always abbreviated as 'RD.'
</br>

```console
100 NORTH MAIN RD.
100 NORTH BRD. RD.
100 NORTH BROAD RD.
100 NORTH BROAD RD.
```
</br>
- <mark>The ＄ means “end of the string.” (There is a corresponding character, the caret ^, which means “beginning of the string.”) Using the re.sub() function, you search the string s for the regular expression 'ROAD＄' and replace it with 'RD.'.</mark> This matches the ROAD at the end of the string s, but does not match the ROAD that’s part of the word BROAD, because that’s in the middle of s.
</br>
- but if the street name was 'BROAD', then the regular expression would match 'ROAD' at the end of the string as part of the word 'BROAD', which is not what I wanted.

</br>
</br>

```python
import re

s = '100 BROAD'
print (re.sub('ROAD$', 'RD.', s))
#'100 BRD.'

print (re.sub('\\bROAD$', 'RD.', s))   #①
#'100 BROAD'

print (re.sub(r'\bROAD$', 'RD.', s))   #②
#'100 BROAD'

s = '100 BROAD ROAD APT. 3'
print (re.sub(r'\bROAD$', 'RD.', s))   #③
#'100 BROAD ROAD APT. 3'

print (re.sub(r'\bROAD\b', 'RD.', s))  #④
#'100 BROAD RD. APT 3'
```
</br>
- console ouput

```console
100 BRD.
100 BROAD
100 BROAD
100 BROAD ROAD APT. 3
100 BROAD RD. APT. 3
```
</br>
- 1) What I really wanted was to match 'ROAD' when it was at the end of the string and it was its own word (and not a part of some larger word). To express this in a regular expression, <mark>you use \b, which means “a word boundary must occur right here.” In Python, this is complicated by the fact that the '\' character in a string must itself be escaped.</mark>
</br>
- 2) To work around the backslash plague, <mark>you can use what is called a raw string, by prefixing the string with the letter r. This tells Python that nothing in this string should be escaped; '\t' is a tab character, but r'\t' is really the backslash character \ followed by the letter t.</mark>
</br>
    ** I recommend always using raw strings when dealing with regular expressions; otherwise, things get too confusing too quickly (and regular expressions are confusing enough already). **
</br>
- ③ Because 'ROAD' isn’t at the very end of the string, it doesn’t match, so the entire call to re.sub() ends up replacing nothing at all, and you get the original string back, which is not what you want.
</br>
- ④ **<mark>To solve this problem, I removed the $ character and added another \b.</mark>**
