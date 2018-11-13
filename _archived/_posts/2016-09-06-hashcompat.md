---
title: Django 1.6 No Longer Supports hashcompat
---

When I tried to run one of my Django projects with Django 1.10, I happened to have the error message as follows:

```shell
...
...
    from django.utils.hashcompat import sha_constructor
ImportError: No module named hashcompat
```

The project itself was designed with Django 1.4. According to [Django Deprecation Timeline](https://django.readthedocs.io/en/1.4/internals/deprecation.html#id4), Django 1.6 or later no longer supports the `hashcompat` module. 

>The compatibility modules django.utils.copycompat and django.utils.hashcompat as well as the functions django.utils.itercompat.all and django.utils.itercompat.any will be removed. The Python builtin versions should be used instead.

So, to deal with the import error, I modified the following line

```python
from django.utils.hashcompat import sha_constructor
```

to

```python
try:
    from django.utils.hashcompat import sha_constructor
except ImportError:
    from haslib import sha1 as sha_constructor
```

and it seems everything works well so far.
