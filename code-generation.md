While the usual way to interact with other languages is to interact through C interfaces in both ATS and the other language, in some cases it may be desirable to directly compile ATS to another language.

Currently, this is possible for the following languages:
* C (The default; several compilers are known to work, including GCC, LLVM/Clang, and TinyCC.)
* Javascript (Compilation is supported by the emscripten compiler which compiles C code to javascript [\[1\]][1].)
* [Python](https://github.com/githwxi/ATS-Postiats-contrib/tree/master/projects/MEDIUM/CATS-parsemit/Python)
* PHP
* Perl

To make a code generator for language X, cd to `$PATSHOME/projects/MEDIUM/CATS-parsemit/X`, run `make` and copy atscc2X to `$PATSHOME/bin`.

### Introduction

ATS2 compiler targets a subset of C programming language. There is a library/utility CATS-parsemit (see above for a link) that parses ATS2 compiler output and transforms it into executable code in other programming languages (e.g., currently, Python).

The subset is comprised by the following kinds of syntax (see atsparemit.sats):

* s0exp (static expressions, for types)
* d0exp (dynamic expressions, i.e. expressions that get executed at run-time to yield values, but not involving any control flow)
* instr (low-level instruction nodes, e.g. if-then-else, return, jump, assignment)
* d0ecl (declarations of types, macros, external functions, and functions compiled from ATS2 source code)

A function declaration (f0decl) consists of function kind (external/static), heading (i.e. signature, that is, list of (named) arguments and return type) and optional body (list of local variable definitions and list of instructions). Moreover, in accordance with C rules, every function is emitted twice: firstly, as a forward-declaration (contains no body, arguments might be unnamed), and secondly, as a definition (in this case, body is present).

### Overview of making an ATS code generator

First clone the [CATS-parsemit directory](https://github.com/githwxi/ATS-Postiats-contrib/tree/master/projects/MEDIUM/CATS-parsemit).

Say you want atscc2XYZ for a language called XYZ.

Create a directory of the name XYZ (or any other name you like) and some symbolic links:

```
mkdir XYZ
cd XYZ
ln -s ../*.?ats .
```

Now you can study atscc2py, atscc2js and atscc2php.

1.  `atscc2py` is the hardest as it does not support (1) `goto` labels or (2) switch statements.
2.  `atscc2php` is the easiest as it supports both (1) and (2).
3.  `atscc2js` is in the middle: it supports (2) but not (1).

### Language translating functions

For more complete documentation, please see:

https://github.com/hsk/docs/blob/master/ats/compiled_c_macro.md

* `ATSINSlab/ATSINSgoto` are used for pattern matching compilation.
* `ATSINSflab/ATSINSfgoto` are used to support tail-call optimization.
* `ATSmove_boxrec(tmp, T)` creates an uninitialized record of the type T, and
assign it to tmp.
* `ATSmove_boxrec` is always followed by a few assignments for field initialization;
they should probably grouped together and then translated into something like:
```python
tmp = (v1, v2, ..., vn) # (python)
```

### Javascript

Simple examples can be tried [on-line](http://www.ats-lang.org/SERVER/MYCODE/Patsoptaas_serve.php?mycode=hello).

Here are steps to generate Javascript from ATS on your own system:

1. Generating the command `atscc2js`. There is a packaged version [on sourceforge](http://sourceforge.net/p/ats2-lang-contrib/code/ci/master/tree/projects/ATSCC2JS/) (also on [github](https://github.com/githwxi/ATS-Postiats-contrib/tree/master/projects/MEDIUM/CATS-parsemit/JavaScript)).

  Use `make` to build. Of course you need `patscc` and `patsopt`.

2. Please take a look at the examples in [this directory](https://github.com/githwxi/ATS-Postiats-contrib/blob/master/projects/MEDIUM/CATS-parsemit/JavaScript/TEST). There is a Makefile there that shows how to generate JS code from ATS source.

  Say you have `foo.dats`. Essentially this is what you need to generate `foo_dats.js`:

  ```
  patsopt -d foo.dats | atscc2js -o foo_dats.js
  ```

### Perl

The directions for the Perl code generator (`atscc2pl`) are similar to the other code generators, but we've included some possible directions for convenience.

```sh
#
# Assumes $PATSHOMERELOC is set to your ATS-Postiats-contrib directory.
#

#Build atscc2pl
cd $PATSHOMERELOC/CATS-parsemit/Perl
make
cp atscc2pl $PATSHOME/bin/

#Build libraries for Perl
cd $PATSHOMERELOC/contrib/libatscc/libatscc2pl
make
make all_in_one
export PERL5LIB=$PERL5LIB:$PATSHOMERELOC/contrib/libatscc/libatscc2pl

```

### Python
For compiling code to Python, there is currently no plan to handle pointer operations.
Or one may go the Cython road.

Because Python does not support jumps, ATSINSgoto and ATSINSfgoto
need to be removed. I will try to do it.



[1]: https://groups.google.com/d/msg/ats-lang-users/WVje4zG4bKA/p-XulrfBFwIJ