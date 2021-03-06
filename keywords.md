### Note: probably a great way to fill in and curate this page is to grep for 'keyword' in the ATS Book, as they are often described as such there.

* `absprop` - introduce a named abstract proposition definition; a specialized form of `sta` [1]; see [[type]].
* `abstype` - introduce a named abstract type definition; a specialized form of `sta` [1]; see [[type]].
* `absview` - introduce a named abstract view definition; a specialized form of `sta` [1]; see [[type]].
* `absviewtype` - introduce a named abstract view type definition; a specialized form of `sta` [1]; see [[type]].
* `absvtype`  - shorter name for `absviewtype`; see [[type]].
* `addr@` - unary operator that takes a variable (see `var` below) and returns a pointer; the view at this
address can be obtained using `view@` (see below).
* `assertloc` - a dynamic assertion (boolean), which prints out its location whenever it evaluates to false; see [migrating a c project to ats on ats.lang.users](https://groups.google.com/forum/#!topic/ats-lang-users/gc-7RtVPCJo).
* `castfn` - a function (`fn`) that changes the type, both dynamically and statically, of its argument. The converted value is returned. When only a static `castfn` is needed, one can use the `cast` and related functions in `unsafe.sats` to save time (a common use is converting a pointer from C to some other viewtype).
* `dataprop` - introduce a named algebraic proposition definition [2]; see [[type]].
* `datatype` - introduce a named algebraic type definition [2]; see [[type]].
* `dataview` - introduce a named algebraic view definition [2]; see [[type]].
* `dataviewtype`  - introduce a named algebraic view type definition [2], a linear data‑type; see [[type]] and [[dataviewtype]].
* `datavtype`  - shorter name for `dataviewtype`; see [[dataviewtype]].
* `dynload` - declare a module initialization dependency, typically from the module defining `main`; see [[dynload]].
* `extern` - declare an entity / definition as extern; the defined item may be a macro or an element in a separate compilation unit; see [[Writing interfaces to C libraries]] and [[C interface]].
* `fn` - non-recursive function (`fun`). Used in place of `fun` for optimization purposes (is this true?) and as well as to check against the possibility of an accidental infinite loop.
* `fun` - a function that can be recursive.
* `infix` - like `symintr`, but with fixity; see [[overload]].
* `infixr` - like `symintr`, but with fixity; see [[overload]].
* `infixl` - like `symintr`, but with fixity; see [[overload]].
* `implement` - used to implement a function that has been defined using `fun` or `fn`
* `of` - has several purposes. Most commonly, it is used as a type specifier in an algebraic constructor (e.g. in a `datatype`). It also can specify the type in some other contexts such as specifying what the ATS type is for an external type (`$extype`; see [[C interface|C interface]]). Finally, it can denote operator overloading precedence (see [[overload|overload#overloading-precedence]]).
* `overload` - overloads a symbol previously introduced with `symintr`; this tells what is overloaded; see [[overload]].
* `postfix` - like `symintr`, but with fixity; see [[overload]].
* `prefix` - like `symintr`, but with fixity; see [[overload]].
* `primplement` - implement a proof function; see [prfun, extern and implement at ats.lang.users](https://groups.google.com/forum/#!topic/ats-lang-users/7-EMCceXpv4); see also `primplmnt`.
* `primplmnt` - implement a proof function; see [prfun, extern and implement at ats.lang.users](https://groups.google.com/forum/#!topic/ats-lang-users/7-EMCceXpv4); see also `primplement`.
* `propdef` - introduce an alias / name for a proposition definition; a specialized form of `stadef` [1]; see [[type]].
* `sif` - like the conditional statement `if`, for static conditional expression (in proofs) ; see [Constructing Proofs as Total Functions, in Intro to ATS](http://ats-lang.sourceforge.net/DOCUMENT/INT2PROGINATS/HTML/x2905.html).
* `sta` - introduce an alias / name for an abstract static definition; there are specialized form of it; see [[type]].
* `stadef` - introduce an alias / name for a concrete static definition; `stadef` is to static what `val` is to dynamic; there are specialized form of it; see [[type]] and [Example: Proving Properties on Braun Trees, in Intro to ATS](http://ats-lang.sourceforge.net/DOCUMENT/INT2PROGINATS/HTML/x3017.html).
* `staload` - either loads a name‑space assigning it to a named prefix or opens a name‑space (anonymously, without a prefix); see [[staload]].
* `symintr` - introduce the name of a symbol (without fixity) to be overloaded (this does not introduce the overloading), with the later help of `overload` and `with`; see [[overload]].
* `tkindef` - `tkindef k = "t"` is the same as `stadef k = $extkind "t"`; see file `basics_sta.sats`.
* `typedef` - introduce an alias / name for a concrete type definition; a specialized form of `stadef` [1]; see [[type]].
* `val` - introduces a val-declaration, which binds a value to a name. This is the most common way of making "variables" in ATS; but see `var` for an alternative.
* `val-` - introduces a val-declaration with additional meaning; if names in a datatype constuctor are being bound (e.g. `val-list_cons(x,xs) = some_list`) then it will suppress a warning message in the case that the pattern matching is non-exhaustive. If instead a value is being matched (e.g. `val-8 = n*4`), this will perform dynamic checking and will error (in this example, the program will exist if n is not equal to 2).
* `val+` - introduces a val-declaration with additional meaning; if names in a datatype constuctor are being bound (e.g. `val+list_cons(x,xs) = some_list`) the warning message about non-exhaustiveness for the pattern matching will be converted into an error. If `val+` is matching a value (as in the `val-` example above, it is similar to `val-`, but will do static checking. This is useful for things like indexed types, but cannot be used in all the cases where dynamic checking can be used.
* `var` - introduces a stack-allocated (local) variable. In contrast to a val-declaration (see `val` above), these variables may be updated or may be declared without being [[initialized|initialization]]. Note, however, that it is fine to overwrite a `val` name with another `val` of the same name. 
* `view@` - unary operator that gives the linear proof (an at-view) of its argument, which should be a variable (`var`); see `addr@` above. 
* `viewdef` - introduce an alias / name for a concrete view definition; a specialized form of `stadef` [1]; see [[type]].
* `viewtypedef` - introduce an alias / name for a concrete view type definition; a specialized form of `stadef` [1]; see [[type]].
* `with` - Has several uses. It can add an overloading to a symbol introduced with `symintr`; this tells with what it is overloaded; see [[overload]]. Also, it is frequently used for certain kinds of aliasing. For instance, it can give an alias to a linear proof: `var y: int with pfy // pfy is an alias of view@(y): int? @ y`
* `withtype` - initiate a style of type annotation. This is a still supported “old” keyword inherited from DML. For more, see: [withtype keyword on ats.lang.users](https://groups.google.com/forum/#!topic/ats-lang-users/5jNYHIRuf6k), [withtype.dats sample](http://www.ats-lang.org/SERVER/MYCODE/Patsoptaas_serve.php?mycode_url=https://raw.githubusercontent.com/githwxi/ATS-Postiats/master/doc/EXAMPLE/TESTATS/withtype.dats) and [JFPmp.pdf](http://www.cs.bu.edu/~hwxi/academic/papers/JFPmp.pdf).

[1]: The latter may be substituted for the former.

[2]: Algebraic à la SML.

## See also

These are not syntactically keywords, but may informally be seen as such. Like keywords, new items can't be created (see [Creating new effects?](https://groups.google.com/forum/#!topic/ats-lang-users/L38Bzie5lsE)) and thus form a fixed set (may still vary with future ATS versions).

* [[Effects|effects]]
* [[Sorts|sort]]
