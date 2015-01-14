Several editors support ATS(2). 

## Editors

### Emacs
* ATS2-mode supports syntax highlighting of ATS and embedded C code. For download, see the [official repository](https://github.com/mrd/ats2-mode) or possible forks ([1](https://github.com/githwxi/ATS-Postiats-contrib/blob/master/contrib/libats-/bbarker/emacs/ats2-mode.el), [2](../tree/master/utils/emacs/ats2-mode.el)).
* ATS2-flymake depends on ATS2-mode. It is available [with ATS2/Postiats](../tree/master/utils/emacs/ats2-flymake.el). It can highlight the location of the source of a type-error pretty well but it may have some room for improvement. Currently, one can use ` C-x `` (that is backquote) to locate the source
of a type-error. Basically, you can do the following (with ats2-mode for emacs being turned on):

```
C-c C-c // for compilation
C-x `     // for locating the source of the first error
C-x `     // for locating the source of the next error
```

### Vim 
There is existing code for a vim mode, but most of the ATS users seem to use emacs. See [this issue](https://github.com/githwxi/ATS-Postiats/issues/30) for a full discussion and code links.

### SublimeText
This is just a syntax highlight file, not a full mode. You can install it at the [Package Control](https://sublime.wbond.net/packages/ATS%20Syntax%20Highlight). 


##IDEs

IDE support is currently in the works. Generally speaking, Java has a number of (free and open source) IDEs that are quite mature (IntelliJ IDEA, Eclipse, Netbeans). There is work on a [parser in Java for ATS](https://github.com/alex-ren/org.ats-lang.postiats.jats). Mostly for historical purposes, there is an [antlr4ide](https://github.com/alex-ren/antlr4ide) supporting ATS.

IDEs outside of the Java ecosystem have also been explored, including [MonoDevelop](https://github.com/ashalkhakov/ATS-Postiats-ide), which currently has syntax highlighting support.

IDE support usually starts with lexing the language into a form that the IDE can understand, and for this purpose, the IDE developer can find the datatype for tokens in ATS2 declared in [pats_lexing.sats](https://github.com/githwxi/ATS-Postiats/blob/master/src/pats_lexing.sats). 

For further discussion on support for IDEs, please see the [google group](https://groups.google.com/forum/#!forum/ats-lang-users).



