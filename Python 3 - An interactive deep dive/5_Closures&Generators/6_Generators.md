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

- ① yield keyword : It is a special kind of function which generates values one at a time. You can think of it as a resumable function.
    - Calling it will return a generator that can be used to generate successive values of x.
- ③ The make_counter() function returns a generator object.
- ④ The next() function takes a generator object and returns its next value.
    - The first time you call next() with the counter generator, it executes the code in make_counter() up to the first yield statement, then returns the value that was yielded.
    - ⑤ Repeatedly calling next() with the same generator object resumes exactly where it left off and continues until it hits the next yield statement.
    - All variables, local state, &c. are saved on yield and restored on next().
- ⑥ The second time you call next(counter), you do all the same things again, but this time x is now 4.

## A fibonacci generator :

</br>

```python
def fib(max):
    a, b = 0, 1          #①
    while a < max:
        yield a          #②
        a, b = b, a + b  #③
```
</br>

- ② a is the current number in the sequence, so yield it.
- ③ b is the next number in the sequence, so assign that to a, but also calculate the next value (a + b) and assign that to b for later use. Note that this happens in parallel.

- **“yield” pauses a function. “next()” resumes where it left off.**

</br>

### Final function would be :
```python
def fib(max):
    a, b = 0, 1          
    while a < max:
        yield a          
        a, b = b, a + b  

for n in fib(1000):      #①
    print(n, end=' ')    #②

#0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987

print (list(fib(1000)))  #③
#[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987]
```
</br>

-  ① You can use a generator like fib() in a for loop directly. The **for loop will automatically call the next() function** to get values from the fib() generator and assign them to the for loop index variable (n).
- ③ This is a useful idiom: pass a generator to the list() function, and it will iterate through the entire generator (just like the for loop in the previous example) and return a list of all the values.
</br>
</br>

## A plural rule generator :

```python
def rules(rules_filename):
    with open(rules_filename, encoding='utf-8') as pattern_file:
        for line in pattern_file:
            pattern, search, replace = line.split(None, 3)                   #①
            yield build_match_and_apply_functions(pattern, search, replace)  #②

def plural(noun, rules_filename='plural5-rules.txt'):
    for matches_rule, apply_rule in rules(rules_filename):                   #③
        if matches_rule(noun):
            return apply_rule(noun)
    raise ValueError('no matching rule for {0}'.format(noun))
```
</br>

- ② And then you yield. What do you yield? Two functions, built dynamically with your old friend, build_match_and_apply_functions()
    - rules() is a generator that spits out match and apply functions on demand.
- ③ Since rules() is a generator, you can use it directly in a for loop. The first time through the for loop, you will call the rules() function, which will open the pattern file, read the first line, dynamically build a match function and an apply function from the patterns on that line, and yield the dynamically built functions.
    - The second time through the for loop, you will pick up exactly where you left off in rules() (which was in the middle of the for line in pattern_file loop).
    - The first thing it will do is read the next line of the file (which is still open), dynamically build another match and apply function based on the patterns on that line in the file, and yield the two functions.

- Advantages : With generators, you can do everything lazily: you read the first rule and create functions and try them, and if that works you don’t ever read the rest of the file or create any other functions.
- Disadvantages : What have you lost? Performance! Every time you call the plural() function, the rules() generator starts over from the beginning — which means re-opening the patterns file and reading from the beginning, one line at a time.

- What if you could have the best of both worlds: minimal startup cost (don’t execute any code on import), and maximum performance. To do that, you’ll need to build your own iterator.