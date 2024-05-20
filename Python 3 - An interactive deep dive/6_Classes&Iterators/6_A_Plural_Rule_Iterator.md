## A Plural Rule Iterator

``` python
class LazyRules:
    rules_filename = 'plural6-rules.txt'

    def __init__(self):
        self.pattern_file = open(self.rules_filename, encoding='utf-8')
        self.cache = []

    def __iter__(self):
        self.cache_index = 0
        return self

    def __next__(self):
        self.cache_index += 1
        if len(self.cache) >= self.cache_index:
            return self.cache[self.cache_index - 1]

        if self.pattern_file.closed:
            raise StopIteration

        line = self.pattern_file.readline()
        if not line:
            self.pattern_file.close()
            raise StopIteration

        pattern, search, replace = line.split(None, 3)
        funcs = build_match_and_apply_functions(
            pattern, search, replace)
        self.cache.append(funcs)
        return funcs

rules = LazyRules()
```

- So this is a class that implements __iter__() and __next__(), so it can be used as an iterator. Then, you instantiate the class and assign it to rules. This happens just once, on import.

- iter(f) calls f.__iter__. next(f) calls f.__next__

Putting it all together, here’s what happens when:

-   When the module is imported, it creates a single instance of the LazyRules class, called rules, which opens the pattern file but does not read from it.
-   When asked for the first match and apply function, it checks its cache but finds the cache is empty. So it reads a single line from the pattern file, builds the match and apply functions from those patterns, and caches them.
-   Let’s say, for the sake of argument, that the very first rule matched. If so, no further match and apply functions are built, and no further lines are read from the pattern file.
-   Furthermore, for the sake of argument, suppose that the caller calls the plural() function again to pluralize a different word. The for loop in the plural() function will call iter(rules), which will reset the cache index but will not reset the open file object.
-   The first time through, the for loop will ask for a value from rules, which will invoke its __next__() method. This time, however, the cache is primed with a single pair of match and apply functions, corresponding to the patterns in the first line of the pattern file. Since they were built and cached in the course of pluralizing the previous word, they’re retrieved from the cache. The cache index increments, and the open file is never touched.
-   Let’s say, for the sake of argument, that the first rule does not match this time around. So the for loop comes around again and asks for another value from rules. This invokes the __next__() method a second time. This time, the cache is exhausted — it only contained one item, and we’re asking for a second — so the __next__() method continues. It reads another line from the open file, builds match and apply functions out of the patterns, and caches them.
-   This read-build-and-cache process will continue as long as the rules being read from the pattern file don’t match the word we’re trying to pluralize. If we do find a matching rule before the end of the file, we simply use it and stop, with the file still open. The file pointer will stay wherever we stopped reading, waiting for the next readline() command. In the meantime, the cache now has more items in it, and if we start all over again trying to pluralize a new word, each of those items in the cache will be tried before reading the next line from the pattern file.