# A List Of Patterns :
</br>

- Let’s factor out the patterns so that defining new rules can be easier.

```python
import re

def build_match_and_apply_functions(pattern, search, replace):
    def matches_rule(word):                                     #①
        return re.search(pattern, word)
    def apply_rule(word):                                       #②
        return re.sub(search, replace, word)
    return (matches_rule, apply_rule)                           #③
```
</br>

- ① build_match_and_apply_functions() is a function that builds other functions dynamically. It takes pattern, search and replace, then defines a matches_rule() function which calls re.search() with the pattern that was passed to the build_match_and_apply_functions() function.
- ② Building the apply function works the same way.
    - the word that was passed to the apply_rule() function you’re building. This technique of using the values of outside parameters within a dynamic function is called closures.
- ③ Finally, the build_match_and_apply_functions() function returns the two functions you just created.
    - The constants you defined within those functions (pattern within the matches_rule() function, and search and replace within the apply_rule() function) stay with those functions, even after you return.
</br>
</br>

## It may become clearer when you see how to use it.

```python
import re
def build_match_and_apply_functions(pattern, search, replace):
  pass
  
patterns = (('[sxz]$','$','es'),('[^aeioudgkprt]h$','$','es'),('(qu|[^aeiou])y$','y$','ies'),('$','$','s'))
          #①                                                                                        #②       
rules = [build_match_and_apply_functions(pattern, search, replace)                                  #③
         for (pattern, search, replace) in patterns]
```
</br>

- ① Our pluralization “rules” are now defined as a tuple of tuples of strings (not functions).
- ② The final regular expression asks whether the word has an end (＄ matches the end of a string).
    - Thus, it serves the same purpose as the match_default() function that always returned True: it ensures that if no more specific rule matches, the code adds an s to the end of the given word.
- ③  This means that rules ends up being functionally equivalent to the previous example: a list of tuples, where each tuple is a pair of functions.
</br>

## The main entry point :

```python
def plural(noun):
    for matches_rule, apply_rule in rules:  #①
        if matches_rule(noun):
            return apply_rule(noun)
```
</br>

- ① It takes a list of rule functions and calls them in order. Now they are built dynamically by mapping the output of the build_match_and_apply_functions() function onto a list of raw strings.

</br>
</br>

## Full code :

```python
import re

def build_match_and_apply_functions(pattern, search, replace):
    def matches_rule(word):                                     #①
        return re.search(pattern, word)
    def apply_rule(word):                                       #②
        return re.sub(search, replace, word)
    return (matches_rule, apply_rule)                           #③

patterns = (('[sxz]$','$','es'),('[^aeioudgkprt]h$','$','es'),('(qu|[^aeiou])y$','y$','ies'),('$','$','s'))
          #①                                                                                        #②       
rules = [build_match_and_apply_functions(pattern, search, replace)                                  #③
         for (pattern, search, replace) in patterns]

def plural(noun):
    for matches_rule, apply_rule in rules:  #①
        if matches_rule(noun):
            return apply_rule(noun)

```
