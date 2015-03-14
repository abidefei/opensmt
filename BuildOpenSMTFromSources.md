# Requirements #

The current districution has been successfully compiled and tested under
Linux and Mac. In order to compile OpenSMT you need:
  * gcc/g++ >= 4.3.2
  * autotools
  * flex
  * bison
  * libtool
  * [The GNU Multiple Precision library](http://gmplib.org) (GMP)

## Quick Tip for Ubuntu Users ##

On Ubuntu 8.10+ (8.04- may have a too old gcc version):

```
sudo apt-get install autoconf libtool g++ bison flex
```

## Download and Install GMP ##

Finally you need to download and install [GMP](http://gmplib.org):

```
wget ftp://ftp.gmplib.org/pub/gmp-4.3.1/gmp-4.3.1.tar.gz
tar xzvf gmp-4.3.1.tar.gz
cd gmp-4.3.1
./configure --enable-cxx
make
sudo make install
cd ..
```

Pay attention to the flag `--enable-cxx` in configuration, necessary for producing C++ linkable library.

# Compile #

From the root directory of OpenSMT:

  * Generate configure
```
autoreconf --install (generates some files and directories. Use --force if you wish to overwrite)
```

  * Create a directory (e.g. build) that will contain the object files and the executable, and change into it
```
mkdir build
cd build
```

  * Generate Makefiles and compile
```
../configure && make
```

You should find an executable `opensmt` in the same directory.


# Special executables #

It is possible to generate special executables, by specifying command-line options to configure:

  * Debugging version: disables optimizations to allow assertion checking
```
../configure --disable-optimization
```

  * SMTCOMP version: no output, except sat/unsat/unknown. Optimizations are turned automatically on
```
../configure --enable-smtcomp
```

  * Profile version
```
../configure --enable-profiling
```

  * Pedantic assertion checking: enables certain SLOW sanity checks during execution. Optimizations must be turned off
```
../configure --enable-pedantic_debug --disable-optimization
```

  * External tool checking (now deprecated): each call to the theory part is checked against an external tool (you need to download "tool\_wrapper.sh" and make sure it is inside a directory included in the PATH variable - not fully supported yet)
```
../configure --enable-external_tool --disable-optimization
```