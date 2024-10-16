# Postscript: Character Encoding Of Python Source Code

- <mark>Python 3 assumes that your source code — i.e. each .py file — is encoded in UTF-8.</mark>
    - In Python 2, the default encoding for .py files was ASCII. <mark>In Python 3, the default encoding is **UTFf-8.**</mark>

- <mark>If you would like to use a different encoding within your Python code, you can put an encoding declaration on the first line of each file. This declaration defines a .py file to be windows-1252:</mark>

```console
# -*- coding: windows-1252 -*-
```

- the character encoding override can also be on the second line, if the first line is a UNIX-like hash-bang command.

```console
#!/usr/bin/python3
# -*- coding: windows-1252 -*-
```
