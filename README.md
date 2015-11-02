**dev is a shell script to be sourced in your profile which enables fast pushing and popping of folders on stacks (colon-separated environment variables such as PATH and PYTHONPATH)**

The main use is pushing one or several "dev" (a folder containing development executables and Python modules to be used in priority) while you iterate on your code, and "popping" them when you're done:

```sh
> dev
Pushed . on PATH
Pushed ./bin on PYTHONPATH
> # Will use executables, python modules from this folder while you work on your code
> undev
Removed . from PATH
Removed ./bin from PYTHONPATH
```

dev tracks which paths have been added to which stack and only removes paths that it has added in order to leave you free to (reasonably) continue modifying your environment variables while you develop. It tries not to interfere with parts of stacks it is not responsible of.

dev also provides functions to push paths to arbitrary stacks:
```sh
> pushOn . LD_LIBRARY_PATH
Pushed . on LD_LIBRARY_PATH 
```

Installation
------------

* clone this repository in a convenient location (e.g. `~/.local`)
* source the dev in your shell profile (e.g. add `. ~/.local/dev/dev` to your `~/.profile`)

Functions
---------

* `dev`: Pushes `$1` on `PATH` and `$1/bin` on `PYTHONPATH`
* `undev`: Pops `$1` from `PATH` and `$1/bin` from `PYTHONPATH`
* `devStatus`: Prints the values of `PATH` and `PYTHONPATH`, as well as the contents of  all tracked stacks
* `pushOn`, `pushPATH`, `pushPYTHONPATH`: Prepends `$1` to the stack named `$2` (fixed to `PATH` and `PYTHONPATH` for the 2 other versions)
* `popFrom`, `popPATH`, `popPYTHONPATH`: Removes `$2` (or the top of the stack by default: pop behavior) from the stack named `$1` (fixed to `PATH` and `PYTHONPATH` for the 2 other versions)
