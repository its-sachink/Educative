</br>
You should now be familiar with the following techniques:
</br>

    - ^ matches the beginning of a string.
    - ＄ matches the end of a string.
    - \b matches a word boundary.
    - \d matches any numeric digit.
    - \D matches any non-numeric character.
    - x? matches an optional x character (in other words, it matches an x zero or one times).
    - x* matches x zero or more times.
    - x+ matches x one or more times.
    - x{n,m} matches an x character at least n times, but not more than m times.
    - (a|b|c) matches exactly one of a, b or c.
    - (x) in general is a remembered group. You can get the value of what matched by using the groups() method of the object returned by re.search.