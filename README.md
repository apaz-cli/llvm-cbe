llvm-cbe
========

Resurrected LLVM C backend, with improvements.


INSTALLATION INSTRUCTIONS
=========================

This version of the LLVM C backend works with LLVM 10.0. Earlier versions are supported too.

Step 1: Installing LLVM
=======================

Either compile LLVM yourself:
-----------------------------
Note: to convert C to LLVM IR to run the tests, you will also need a C compiler using the LLVM infrastructure, such as clang.

The first step is to compile LLVM on your machine
(this assumes an in-tree build, but out-of-tree will also work):

     cd $HOME
     git clone https://github.com/llvm/llvm-project.git
     cd llvm-project
     git checkout release/8.x
     mkdir llvm/build
     cd llvm/build
     cmake ..
     make

Or install the LLVM packages on your system:
--------------------------------------------

On macOS, use pkgsrc and install the llvm package. On CentOS, install the llvm-devel package.

Step 2: Compiling LLVM-CBE
==========================

Next, download and compile llvm-cbe from the same folder if you built LLVM yourself, or where you'd like in the other case:

    cd $HOME/llvm-project/llvm/projects
    git clone https://github.com/JuliaComputing/llvm-cbe
    cd ../build
    cmake ..
    make llvm-cbe

To run tests, you will also need to build `lli`:

```sh
    make lli
```

Step 3: Usage Examples
======================

If llvm-cbe compiles, you should be able to run it with the following commands.
```
$ cd $HOME/llvm-project/llvm/projects/llvm-cbe/test/selectionsort
$ ls
main.c
$ clang -S -emit-llvm -g main.c
$ ls
main.c main.ll
$ $(HOME)/llvm/build/bin/llvm-cbe main.ll
```

Compile Generated C-Code and Run
================================

```
$ gcc -o main.cbe main.cbe.c
$ ls
main.c  main.cbe  main.cbe.c  main.ll
$ ./main.cbe
```

Running tests
==================

Unit tests:

```sh
    $ cd $HOME/llvm-project/llvm/build
    $ make CBEUnitTests && projects/llvm-cbe/unittests/CWriterTest
```

Other tests:

First, compile llvm-cbe, and install pytest. Then:

```sh
    $ cd $HOME/llvm-project/llvm/projects/llvm-cbe
    $ pytest
```

You might have to adjust the llvm-cbe and lli paths in that configuration.
