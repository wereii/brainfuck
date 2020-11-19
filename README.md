#        BRAINFUCKCC

	A(nother) Brainfuck compiler

## INSTALL

```shell
mkdir build
cd build
cmake ..
make
# make test
sudo make install
```

Installation location can be specified with:

	cmake -DCMAKE_INSTALL_PREFIX=/usr

Where this would result into `/usr/bin/bfcc`, 
and defaults (depending on your cmake version)
to `/usr/local`.

### DEPENDENCIES

    gcc
    binutils (ld, as - runtime dependency) 

Cmake script checks for these and will warn you if they are missing.

## NOTES

This is just a fork of https://github.com/benjamin-james/brainfuck.
Main compilation logic comes from James's version,
I've only used is as a base for my own doings
(fixing a few, adding a bit etc, see commit history).
