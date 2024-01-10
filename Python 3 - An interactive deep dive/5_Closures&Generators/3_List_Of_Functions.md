# A List Of Functions :
</br>

```python
import re

def match_sxz(noun):
    return re.search('[sxz]$', noun)

def apply_sxz(noun):
    return re.sub('$', 'es', noun)

def match_h(noun):
    return re.search('[^aeioudgkprt]h$', noun)

def apply_h(noun):
    return re.sub('$', 'es', noun)

def match_y(noun):                             #①
    return re.search('[^aeiou]y$', noun)
        
def apply_y(noun):                             #②
    return re.sub('y$', 'ies', noun)

def match_default(noun):
    return True

def apply_default(noun):
    return noun + 's'

rules = ((match_sxz, apply_sxz),               #③
         (match_h, apply_h),
         (match_y, apply_y),
         (match_default, apply_default)
         )

def plural(noun):           
    for matches_rule, apply_rule in rules:       #④
        if matches_rule(noun):
            return apply_rule(noun)
```
</br>

- ① Now, each match rule is its own function which returns the results of calling the re.search() function.
- ② Each apply rule is also its own function which calls the re.sub() function to apply the appropriate pluralization rule.
- The reason this technique works is that everything in Python is an object, including functions. The **rules data structure contains functions — not names of functions, but actual function objects**.
    - When they get assigned in the for loop, then matches_rule and apply_rule are actual functions that you can call.
</br>
</br>

- The entire for loop is equivalent to :

```python
def plural(noun):
    if match_sxz(noun):
        return apply_sxz(noun)
    if match_h(noun):
        return apply_h(noun)
    if match_y(noun):
        return apply_y(noun)
    if match_default(noun):
        return apply_default(noun)
```