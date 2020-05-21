# Embedded Python Notes

**You can now use Python's own embedded/standalone python distro: https://www.python.org/downloads/windows/** . This repository only contains some information on using/modifying it.

## What is this?

This repository has some documentation on how to modify a custom embedded python, and gotchas when using it.

## How do I modify the default embedded python distribution?

As an example, we'll add the tkinter package

- Download the non-embedded version of python from main python website: https://www.python.org/downloads/windows/ 
- Install python (recommend "all users" so it's easy to find the path) 
- Copy these files out of the normal python install (I followed [these instructions](https://stackoverflow.com/questions/37710205/python-embeddable-zip-install-tkinter/44169516):
  - the tcl folder
  - the tkinter folder
  - tcl86t.dll
  - tk86t.dll
  - _tkinter.pyd
- copy all these into the embedded python root folder

### Adding packages as zip files

If a package only contains python scripts, you can add it as a zip file (but it's not always a good idea):

- zip your packages into `example_archive.zip`, and copy it into embedded python root folder. It should contain a folder for each package you want to include.
- copy any non-python scripts (like .dll files) into the embedded python root folder
- modify the `python37._pth` file - add the name of the zip to import on startup `example_archive.zip` (whatever you called your .zip file before)

If you have any issues, try using it without a zip file first to see if the zip file is causing problems. You probably only want to use zip files if there are hundreds of python scripts.

## Gotchas

- Python embedded will only look at files adjacent to the .exe, and in the python37.zip file, due its `python37._pth`. This is on purpose to system libraries interfering with its operation. If you wish to change this, you can do the following
  - If you want to import your own packages, you can either put them next to the .exe, or you can manually add them to your sys.path (just a list).
```
import sys
import os

sys.path.append(os.getcwd()) # allow imports from the directory where python is being run from
sys.path.append("c:/path/to/scan/for/libraries") # add any other paths you want to scan
print(sys.path) # check that the paths seem correct
```

- Embedded python also seems to use a different `Lib/site.py` (see https://docs.python.org/3/library/site.html). This means 'special' functions like `exit()` are not imported by default - you need to use sys.exit(), or raise SystemExit, [see here](https://stackoverflow.com/questions/19747371/python-exit-commands-why-so-many-and-when-should-each-be-used) . This can break many scripts as they usually assume these functions are present.
