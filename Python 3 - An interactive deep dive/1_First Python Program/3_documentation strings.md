# Writing Readable Code

## Documentation strings

You can document a Python function by giving it a documentation string (docstring for short). In this program, the approximate_size() function has a docstring:

```python
def approximate_size(size, a_kilobyte_is_1024_bytes=True):
    '''Convert a file size to human-readable form.

    Keyword arguments:
    size -- file size in bytes
    a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024
                                if False, use multiples of 1000

    Returns: string

    '''
```

<mark> Triple quotes signify a multi-line string. </mark> Everything between the start and end quotes is part of a single string, including carriage returns, leading white space, and other quote characters.

Every function deserves a decent docstring. Everything between the triple quotes is the function’s docstring, which documents what the function does. <mark> A docstring, if it exists, must be the first thing defined in a function (that is, on the next line after the function declaration). </mark>