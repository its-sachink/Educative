# A File Of Patterns :
</br>

- The next logical step is to take these strings and put them in a separate file, where they can be maintained separately from the code that uses them.
</br>

```console
# cat plural4-rules.txt
[sxz]$               $    es
[^aeioudgkprt]h$     $    es
[^aeiou]y$          y$    ies
$                    $    s
```
</br>

- Let's see how to use this rules file.
</br>

```python
import re

def build_match_and_apply_functions(pattern, search, replace):     #①
    def matches_rule(word):
        return re.search(pattern, word)
    def apply_rule(word):
        return re.sub(search, replace, word)
    return (matches_rule, apply_rule)

rules = []
with open('plural4-rules.txt', encoding='utf-8') as pattern_file:  #②
    for line in pattern_file:                                      #③
        pattern, search, replace = line.split(None, 3)             #④
        rules.append(build_match_and_apply_functions(              #⑤
                pattern, search, replace))
       
```
</br>

- ④ To split it out, use the split() string method. The first argument to the split() method is None, which means “split on any whitespace (tabs or spaces, it makes no difference).”
    - The second argument is 3, which means “split on whitespace 3 times, then leave the rest of the line alone.”
    - A line like [sxz]＄ ＄ es will be broken up into the list ['[sxz]＄', '＄', 'es'], which means that pattern will get '[sxz]＄', search will get '＄', and replace will get 'es'.

- ⑤ Finally, you pass pattern, search, and replace to the build_match_and_apply_functions() function, which returns a tuple of functions.
    - You append this tuple to the rules list, and rules ends up storing the list of match and apply functions that the plural() function expects.
- The improvement here is that you’ve completely separated the pluralization rules into an external file, so it can be maintained separately from the code that uses it.