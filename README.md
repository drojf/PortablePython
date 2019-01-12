# PLEASE READ FIRST

It has come to my attention that you can get a fairly small distribution of python just by downloading the 'Zero' version of WinPython (their official stripped down version). I now recommend doing the following, instead of using this repository.

- Download the latest 'Zero' version of WinPython (64 or 32 bit as desired): https://winpython.github.io/
- Run the executable to extract the files
- Take out only the 'python' folder containing the main python distribution. Within that folder:
  - Delete the 'Doc' folder (saves about 8mb), unless you really need the python documentation
  - Delete all \_\_pycache\_\_ folders. I'm not sure whether I had those because I had run python before, or if it already existed after extraction.

After doing this and compressing the python folder using .7z, the archive is around 14 MB. 

Note that if you just use plain .zip, the size will be much larger, since each file will be compressed individually. If you want to use some other archive container which doesn't support archiving files together, it's recommended to TAR it first (to get .tar.gz or .tar.zip), or to zip with STORE mode, then zip the STORE mode .zip file again.

Perhaps in the future I will make a script which does this automatically.

# PortablePython
Portable Python which can be run without installing (based off WinPython)

# Download / Binaries
See the releases section: [Releases](https://github.com/drojf/PortablePython/releases)
