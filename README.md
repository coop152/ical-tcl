Compilation, as of `<CURRENT YEAR>`
---
0. Install a C++ compiler and Tcl/Tk libraries. On Ubuntu, the Tcl/Tk packages are `tcl-dev` and `tk-dev`.
1. Find the location of your Tcl/Tk libraries. We need the directories containing the files `tclConfig.sh` and `tkConfig.sh`, as well as the header files (look for `tcl.h` and `tk.h`). On Ubuntu these are `/usr/lib/tcl8.6` and `/usr/lib/tk8.6` for the config files, and `/usr/include/tcl8.6` for the header files.
2. Run the `configure` script, with these arguments:
```sh
./configure --prefix=/home/<username> --with-tclconfig=<tclConfig Location> --with    -tkconfig=<tkConfig Location> CPPFLAGS=-I<Include Location
```
On Ubuntu, the command would be:
```sh
./configure --prefix=/home/<username> --with-tclconfig=/usr/lib/tcl8.6 --with-tkconfig=/usr/lib/tk8.6 CPPFLAGS=-I/usr/include/tcl8.6
```
3. Run `make` and then `make install`. Note that the program will not work unless installed.
4. Done!

Remark(s)
---
- The prefix given in the configure command seems to be where it installs to. It may be more appropriate to use `/home/<username>/.local`?