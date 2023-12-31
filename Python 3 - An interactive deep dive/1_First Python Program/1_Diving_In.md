# Diving In

Sample program :

```python
SUFFIXES = {1000: ['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'],
            1024: ['KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']}

def approximate_size(size, a_kilobyte_is_1024_bytes=True):
    '''Convert a file size to human-readable form.

    Keyword arguments:
    size -- file size in bytes
    a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024
                                if False, use multiples of 1000

    Returns: string

    '''
    if size < 0:
        raise ValueError('number must be non-negative')

    multiple = 1024 if a_kilobyte_is_1024_bytes else 1000
    for suffix in SUFFIXES[multiple]:
        size /= multiple
        if size < multiple:
            return '{0:.1f} {1}'.format(size, suffix)

    raise ValueError('number too large')

if __name__ == '__main__':
    print(approximate_size(1000000000000, False))
    print(approximate_size(1000000000000))

```

The output will look something like this:

```
1.0 TB
931.3 GiB
```

- The script defines a single function, the approximate_size() function, which takes an exact file size in bytes and calculates a “pretty” (but approximate) size.
- If you display a folder of documents as a multi-column list, it will display a table with the document icon, the document name, the size, type, last-modified date, and so on.
-  If the folder contains a 1093-byte file named TODO, your file manager won’t display TODO 1093 bytes; it’ll say something like TODO 1 KB instead.

<<<<<<< HEAD
=======
![test screenshot](../images/Screenshot_1.jpg)
>>>>>>> 71eccf22914341f9e187e55ee523ade4496fd7e9
