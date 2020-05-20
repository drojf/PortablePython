# Embedded Python with Tkinter

## What is this?

This server hosts a customized version of the embedded python for Windows which you can get from [the python website](https://www.python.org/downloads/windows/). It adds tkinter which is nost present in the default embedded python zip, and is a .7z file instead of a .zip file.

This repository also has documentation on how the custom embedded python was created, and documentation on gotchas when using it.

It is the 32-bit version for maximum compatability. You can follow the below instructions if you want to make a 64-bit version.

## [Click here for Download / Binaries / Releases](https://github.com/drojf/PortablePython/releases)

[Click here for Download / Binaries / Releases](https://github.com/drojf/PortablePython/releases)

## Why not use the default embedded python .zip?

I would like to keep an archive of Python which I can use in future projects, along with documentation of any gotchas/issues which may come up when using it.

Also, if you need tkinter, this project has it built in, while the default embedded python releases do not.

## How was it created?

- Download the non-embedded version of python from main python website: https://www.python.org/downloads/windows/ 
- Install python (recommend "all users" so it's easy to find the path) 
- Copy these files out of the normal python install (I followed [these instructions](https://stackoverflow.com/questions/37710205/python-embeddable-zip-install-tkinter/44169516):
  - the tcl folder
  - the tkinter folder
  - tcl86t.dll
  - tk86t.dll
  - _tkinter.pyd
- Option A:
  - zip the tcl and tkinter folders into `tkinter.zip`, copy into embedded python root folder
  - copy the remaining files int embedded python root folder
  - modify the `python37._pth` file - add the name of the zip to import on startup `tkinter.zip`
- Option B:
  - just copy all the files into the embedded pyhton root folder. This can make copying the python folder slow, even on a SSD as there will be many files included for tkinter

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
