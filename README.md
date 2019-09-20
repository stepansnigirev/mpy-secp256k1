# Micropython bindings for secp256k1 library

## How to compile Micropython with this module

Create a folder for the build and `cd` to it:
```
mkdir my_mpy_build
cd my_mpy_build
```

Clone micropython repo, init submodules:
```
git clone https://github.com/micropython/micropython.git
cd micropython
git submodule update --init
```

Try to compile micropython for your board. Follow the corresponding instructions (readme file in `ports/<board type>`).

When you are able to build and flash micropython to the board you can add user modules to it:

Navigate to the `my_mpy_build` folder, create a `usermods` folder there. Clone modules you want to this folder.
```
mkdir usermods
cd usermods
git clone --recursive https://github.com/diybitcoinhardware/micropython-secp256k1.git
```

In the boards `mpconfigport.h` file add the definition to include the module:
```
#define MODULE_SECP256K1_ENABLED    (1)
```

or just make -DMODULE_SECP256K1_ENABLED=1

Also edit the `Makefile` and remove `-Wall` flag for compilation. Otherwise warnings and unused functions will be treated as errors and compilation will fail.

_FIXME: should be fixed instead..._

```
my_mpy_build/
   micropython/
   usermods/
       /mpy-secp256k1
```

First make sure you can compile micropython from the source code.

Read the documentation for your board in [micropython repo](https://github.com/micropython/micropython/).

Should be something like:

```
cd micropython/mpy-cross
make
cd ../