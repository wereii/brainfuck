#        BRAINFUCKCC

	A(nother) Brainfuck compiler

The compilation itself is forked/taken from 
[Benjamin James's](https://github.com/benjamin-james/brainfuck)
brainfuck compiler. Where the brainfuck code is "converted" into GNU assembly,
compiled using `as` into .o object format and then linked into binary ELF
with GNU `ld`.

## BUILD & INSTALL

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
I've only used it as a base for my own doings
(fixing a few, adding a bit etc, see commit history).
