## ATS Compiler
atscc, sometimes called patscc in ATS/Postiats, is a wrapper utility to allow easier compilation of ATS source code than by using patsopt directly.

Here is more information on 'patscc' and 'patsopt':

http://www.ats-lang.org/Resources.html#ATS-Toolkit

In order to compile ATS2 programs, you can now do
something like:

```
patscc -o test test.dats test_header.sats test_helper.dats
```

For considerably large and complex projects (involving both ATS code and C code), it may be beneficial to use 'patsopt' directly in a Makefile. In most cases, 'patscc' is adequate for handling the compilation of ATS code.


## Build systems

### Using Makefiles

While using Makefiles is both the most common way to compile ATS programs and is also used in the standard way, there are a couple of Makefiles that can be included in ATS programs to make building ATS programs quick: search for examples that include [atsmake-pre.mk](../../tree/master/share/atsmake-pre.mk) and/or [atsmake-post.mk](../../tree/master/share/atsmake-post.mk).

### Using CMake
[Read the docs](https://ats-cmake-documentaition.readthedocs.org/en/latest/index.html) for [ATS-CMake](https://github.com/steinwaywhw/ATS-CMake).

### Using Gradle

Gradle is, along with Makefiles, currently being used for building JNI applications (mixing Java and ATS code). One example is [a calculator application](https://github.com/bbarker/BIBCalc). It is also being used to make available a [simple wrapper for Makefiles](https://gist.github.com/bbarker/c73ecf257bca966c1efd) that allows ATS projects using standard Makefiles to be be used within Java IDEs, like [IntelliJATS](https://github.com/bbarker/IntelliJATS).

## Compiling Portable Code

Several example exist where a Makefile for an ATS project can generate portable C code that can later be compiled without the aid of any ATS installation:

* The most [basic example](../../tree/master/doc/EXAMPLE/PORTABLE).