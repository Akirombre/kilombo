# ckbsim - C kilobot simulator

Authors: Fredrik Jansson, Matthew Hartley, Martin Hinsch, 
         Tjelvar Olsson, Ivica Slavkov, Noemí Carranza

Contact: 
Fredrik Jansson: fjansson@abo.fi
Matthew Hartley: Matthew.Hartley@jic.ac.uk


This repository holds the code for ckbsim, a C based kilobot simulator. The simulator was developed in the [Swarm Organ project](www.swarm-organ.eu), and is distributed under the MIT license (see the file LICENSE for details). Installation instructions follow below. For detailed usage instruction and programming documentation, see `docs/manual.md` and the example bots in `examples/`.



## Prerequisites
You'll need to have:
- git
- cmake
- SDL 1.X (including headers for building, i.e. devel packages under linux)
- the [Jansson library](http://www.digip.org/jansson/) (though it's in many package managers. Again, get the development package)
- the [Check unit testing library](http://check.sourceforge.net/)

Additionally, to compile the code for real kilobots as well, the following are needed:
- avr-gcc (c compiler for the AVR microcontroller, to compile for the kilobot)
- [Kilolib](https://github.com/acornejo/kilolib) (the official Kilobot library)


### Debian-based Linux systems
`sudo apt-get install build-essential git gcc-avr gdb-avr binutils-avr avr-libc avrdude libsdl1.2-dev libjansson-dev cmake check`

### OSX systems (incomplete)

check library:
`brew install check`

Sometimes, need to compile with
`C_INCLUDE_PATH=/usr/local/include/ make`
for the libraries to be found.

## Build instructions

Make a build directory:

	mkdir build
	cd build

Run cmake:

	cmake ..

Install:

	sudo make install

This installs the kilobot simulator in a system-wide location, by default
under `/usr/local/lib` and `/usr/local/include`.


## Compile and run examples
cd examples
cd orbit
make     # or make -f Makefile.osx on OSX
./orbit -b start_positions.json

The example makefiles are set up to build the code for the simulator by default. By running
    make hex
the same source code is compiled for the real Kilobot. This requires the avr-gcc toolchain
and the official Kilolib to be installed (see prerequisites above). The path to Kilolib
needs to be specified in the Makefile.



Note: the simulator uses the [SDL_GFX library](http://cms.ferzkopp.net/index.php/software/13-sdl-gfx)
by Andreas Schiffler (distributed under the zlib license). The source
code for the sdl_gfx library is bundled with the simulator due to its
unreliable availability in various Linux distributions. It is located in the
directory src/gfx, and is automatically compiled with the rest of the
source code.

The simulator also includes the API definitions of kilolib, the C
library for the physical kilobot robot. These are located in the file
src/kilolib.h, with minor, simulator-specific changes.
The full kilolib source code is here: https://github.com/acornejo/kilolib .
