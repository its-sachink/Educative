# Using The {n,m} Syntax :

```python 
import re
pattern = '^M?M?M?$'
print (re.search(pattern, 'M'))     #①
#<_sre.SRE_Match object at 0x008EE090>

print (re.search(pattern, 'MM'))    #②
#<_sre.SRE_Match object at 0x008EEB48>

print (re.search(pattern, 'MMM'))   #③
#<_sre.SRE_Match object at 0x008EE090>

print (re.search(pattern, 'MMMM'))  #④ 
#None
```
</br>

- Alternative to above code can be as below,

```python
import re
pattern = '^M{0,3}$'                #①
print (re.search(pattern, 'M'))     #②
#<_sre.SRE_Match object at 0x008EEB48>

print (re.search(pattern, 'MM'))    #③
#<_sre.SRE_Match object at 0x008EE090>

print (re.search(pattern, 'MMM'))   #④
#<_sre.SRE_Match object at 0x008EEDA8>

print (re.search(pattern, 'MMMM'))  #⑤
#None
```
</br>
```console
<_sre.SRE_Match object; span=(0, 1), match='M'>
<_sre.SRE_Match object; span=(0, 2), match='MM'>
<_sre.SRE_Match object; span=(0, 3), match='MMM'>
None
```
</br>

- ① This pattern says: “Match the start of the string, then anywhere from zero to three M characters, then the end of the string.” The 0 and 3 can be any numbers; if you want to match at least one but no more than three M characters, you could say M{1,3}.

</br>
</br>

- Similarly a pattern matching below can be written alternatively, 

``` console
pattern = '^M?M?M?(CM|CD|D?C?C?C?)(XC|XL|L?X?X?X?)(IX|IV|V?I?I?I?)$'
```
</br>

```python 
import re
pattern = '^M{0,3}(CM|CD|D?C{0,3})(XC|XL|L?X{0,3})(IX|IV|V?I{0,3})$'
print (re.search(pattern, 'MDLV') )             #①
#<_sre.SRE_Match object at 0x008EEB48>

print (re.search(pattern, 'MMDCLXVI') )         #②
#<_sre.SRE_Match object at 0x008EEB48>

print (re.search(pattern, 'MMMDCCCLXXXVIII'))   #③
#<_sre.SRE_Match object at 0x008EEB48>

print (re.search(pattern, 'I'))                 #④
#<_sre.SRE_Match object at 0x008EEB48>
```
