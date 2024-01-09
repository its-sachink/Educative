# Case Study : Roman Numerals

```python 
import re
pattern = '^M?M?M?$'                #①
print (re.search(pattern, 'M'))     #②
#<_sre.SRE_Match object at 0106FB58>

print (re.search(pattern, 'MM'))    #③
#<_sre.SRE_Match object at 0106C290>

print (re.search(pattern, 'MMM'))   #④
#<_sre.SRE_Match object at 0106AA38>

re.search(pattern, 'MMMM')          #⑤
print (re.search(pattern, ''))      #⑥
#<_sre.SRE_Match object at 0106F4A8>
```
</br>
```console
<_sre.SRE_Match object; span=(0, 1), match='M'>
<_sre.SRE_Match object; span=(0, 2), match='MM'>
<_sre.SRE_Match object; span=(0, 3), match='MMM'>
<_sre.SRE_Match object; span=(0, 0), match=''>
```
</br>
- ① This pattern has three parts. ^ matches what follows only at the beginning of the string. You want to make sure that the M characters, if they’re there, are at the beginning of the string.
    - M? optionally matches a single M character. Since this is repeated three times, you’re matching anywhere from zero to three M characters in a row.
    - nd ＄ matches the end of the string. When combined with the ^ character at the beginning, this means that the pattern must match the entire string, with no other characters before or after the M characters.
- ② The essence of the re module is the search() function, that takes a regular expression (pattern) and a string ('M') to try to match against the regular expression. If a match is found, search() returns an object which has various methods to describe the match.
    - if no match is found, search() returns None, the Python null value.
- ③ 'MM’ matches because the first and second optional M characters match and the third M is ignored.
- ④ 'MMM' matches because all three M characters match.
- ⑤ 'MMMM' does not match. All three M characters match, but then the regular expression insists on the string ending (because of the ＄ character).
- ⑥ Interestingly, an empty string also matches this regular expression, since all the M characters are optional.

</br>
</br>
</br>
</br>

```python import re
pattern = '^M?M?M?(CM|CD|D?C?C?C?)$'          #①
print (re.search(pattern, 'MCM') )            #②
#<_sre.SRE_Match object at 01070390>

print (re.search(pattern, 'MD') )             #③
#<_sre.SRE_Match object at 01073A50>

print (re.search(pattern, 'MMMCCC'))          #④
#<_sre.SRE_Match object at 010748A8>

re.search(pattern, 'MCMC')                    #⑤
print (re.search(pattern, ''))                #⑥
#<_sre.SRE_Match object at 01071D98>
```
</br>
```console 
<_sre.SRE_Match object; span=(0, 3), match='MCM'>
<_sre.SRE_Match object; span=(0, 2), match='MD'>
<_sre.SRE_Match object; span=(0, 6), match='MMMCCC'>
<_sre.SRE_Match object; span=(0, 0), match=''>
```
</br>
- ① In parentheses, which defines a set of three mutually exclusive patterns, separated by vertical bars: CM, CD, and D?C?C?C? (which is an optional D followed by zero to three optional C characters). The regular expression parser checks for each of these patterns in order (from left to right), takes the first one that matches, and ignores the rest.
- ② 'MCM' matches because the first M matches, the second and third M characters are ignored, and the CM matches (so the CD and D?C?C?C? patterns are never even considered).
- ③ 'MD' matches because the first M matches, the second and third M characters are ignored, and the D?C?C?C? pattern matches D.
- ④ 'MMMCCC' matches because all three M characters match, and the D?C?C?C? pattern matches CCC (the D is optional and is ignored).
- ⑤ 'MCMC' does not match. The first M matches, the second and third M characters are ignored, and the CM matches, but then the ＄ does not match because you’re not at the end of the string yet (you still have an unmatched C character).
- ⑥ Interestingly, an empty string still matches this pattern, because all the M characters are optional and ignored, and the empty string matches the D?C?C?C? pattern where all the characters are optional and ignored.

