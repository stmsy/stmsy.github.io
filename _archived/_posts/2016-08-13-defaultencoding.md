---
title: Change Default Encoding for Python
#categories: [Python]
#tags: [piney-virtualenv]
---

<!---
1. Check default encoding
2. Change default encoding
--->

## Check Default Encoding

Open the Python interpreter such as [bpython](http://www.bpython-interpreter.org/) or [IPython](https://ipython.org/) and see the default encoding is set ASCII:

```python
>>> import sys
>>> sys.getdefaultencoding()
>>> 'ascii'
```

## Change Default Encoding

You could try 

```python
>>> reload(sys)
>>> sys.setdefaultencoding('utf-8')
```

but you have to reload the `sys` module and set the default encoding every time you open the Python intepreter. To avoid this you could edit/locate `sitecustomize.py` under `usr/lib/python2.7/` (this may depend on the operating system or distribution you are using), or under `~/.pyenv/versions/2.7.12/lib/python2.7/site-packages/` in case you use a virtual environment like [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv), with the following included:

```python
try:
    import sys
    sys.setdefaultencoding('utf-8')
except:
    pass
```
