# `__PATHS__`
a Personal package for me

automatically append paths to sys.path

mange sys.path package
## info
when installing and setuping. no need to import it


# installation

Run the following to install:
```cmd
pip install __PATHS__
```
### or
```cmd
python -m pip install __PATHS__
```
if that didn't work, try replacing `pip` with `pip3`.
need help? my discord: [lab](https://discord.gg/vzEZnC7CM8)

## start
when python starts it import some modules. so we're going to inject code
### you need to add this code to one of the modules
i am going to add it to the site.py module at line 90
```py
def initPaths():
    # this func is not part of site.py module this func been added by The User
    sys.modules["__PATHS__"] = __import__("__PATHS__")
    sys.modules["_traceback"] = __import__("traceback")
    __PATHS__ = sys.modules["__PATHS__"]
    if __PATHS__.settings.auto():
        __PATHS__.__start__()
    if __PATHS__.settings.exex() and __PATHS__.settings.execit():
        try:
            __PATHS__.exec_globals = {'__builtins__': __builtins__}
            __PATHS__.exec_locals  = {'__builtins__': __builtins__}
            exec(__PATHS__.settings.load()["exec"],
                __PATHS__.exec_globals,__PATHS__.exec_locals)
        except Exception:
            sys.modules["_traceback"].print_exc()

initPaths()
```

## append path to sys.paths
```py
>>> import __PATHS__
>>> __PATHS__.append(["E:\\projects\\packages"]) # append paths to sys.path
```
> **Note**
> this must be use every time. if you want to auto append use DumpPaths and set the setting to auto
## dump a path to `_packages_.json`
```py
>>> import __PATHS__
>>> __PATHS__.DumpPaths(["E:\\projects\\packages"])
>>> __PATHS__.settings.init(auto=True) # now it will always add the paths to sys.path
```
### or 
```py
>>> import __PATHS__
>>> __PATHS__.DumpPaths(["E:\\projects\\packages"])
>>> __PATHS__.__start__() # this will replace sys.path with _packages_.json paths
```


## add exec code
```py
import __PATHS__
code = """
print("i see starting the file :)")
import json
import os
print("import everything :O")
"""
__PATHS__.settings.init(exec=code,execit=True,auto=True) # when python imports X. this code will be exec
```
## get exec code locals
```R
E:\projects>python -q
i see starting the file :)
import everything :O
>>> import __PATHS__
>>> import sys
>>> locals().update(sys.modules["__PATHS__"].exec_locals) # update locals with the exec code locals. 
>>> json # you may get an error if you didnt set the setting to exec=code or the exec code was empty
<module 'json' from 'E:\\python\\Python39\\lib\\json\\__init__.py'>
```
