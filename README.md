# Erlang wrapper for SQLite3

This library allows you to work with SQLite3 databases from Erlang.

It is compatible with Windows and Linux, and should probably work on other OSes as well.

## Requirements

Erlang/OTP R14B is required, and SQLite 3 minimum version is 3.6.1.

## Compiling

### Linux

1. Install SQLite3 by running `sudo apt-get install sqlite3` or the equivalent for your package manager, or by [compiling from the source](http://source.online.free.fr/Linux_HowToCompileSQLite.html).

2. `make`.

### Cross-compiling

If you want to use erlang-sqlite3 on an embedded device, it can be cross-compiled.

1. Cross-compile [SQLite3](http://www.sqlite.org/cvstrac/wiki?p=HowToCompile) and [Erlang](http://www.erlang.org/doc/installation_guide/INSTALL-CROSS.html).

2. Change variables and paths in `rebar.cross_compile.config.sample` to the desired values and rename it to `rebar.cross_compile.config`.

3. `make cross_compile`.

### Windows with MS Visual C++

1. Download both the source amalgamation and the precompiled binary from http://www.sqlite.org/download.html. Extract files `sqlite3.h` from the amalgamation and `sqlite3.def` from the binary. Run this command from Visual Studio command prompt:

       lib /def:sqlite3.def

   to create the import library `sqlite3.lib`. In `rebar.config`, set the correct paths in tuples `{"win32", "CFLAGS", "/Idirectory/containing/sqlite3.h/ /Ic_src /W4 /wd4100 /wd4204"}` and `{"win32", "LDFLAGS", "/path/to/sqlite3.lib"}`.

2. `nmake`.

## DLL search path

Note that on Windows, `sqlite3.dll` usually won't be installed in the system-wide DLL search path. In this case, it should be placed in the working directory of your application.

## Running the test suite

### Linux

`make test`

### Windows

1. `nmake tests`

2. If you get the error `"Error loading sqlite3_drv: The specified module could not be found"`, this is because `sqlite3.dll` isn't in the search path. Copy it to the `.eunit` directory.

## Example usage

See tests `src/sqlite3_test.erl` for a starting point.

## Authors

See ./AUTHORS
