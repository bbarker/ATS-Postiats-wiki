## Kiwamu Okabe's practice

On real world, there are not meaning. There are values only.
Meaning is located at a mind of human who watch the values.
Then, it's nonsense that you think type constructor creates values. The order is reversed.

Let's think that a human applies type imagined, by himself, to the value. It's called "Applied Type".
What is value? Value is possible to change any time.
However, the human wishes the value's meaning doesn't change, while the value is changed.
That is to say any things are built with 2 parts, that changing part and fixed part.
The former is "dynamics", the latter is "statics" that is also called "static meaning". Meaning is "type".
Of course, his wish may be sometimes not fitted together.
Types applied wildly by him will not be well-typed.

Whereat, introduce type influence after he applied type.
Any subset of the world should have only a meaning.
If there is some subsets have some meanings, he does not correctly understand the world.
This is Applied Type System.

Also, you could understand it as a complex water pipe maze.
Water is flowing in a water pipe, that is, static and not changed.
And there is only a pipe in same place, if it's not under quantum mechanics.

This attitude can do away with any constructor on the type system.
There is value in the first place. Beautiful.

Also, you could easily make "reference" using "pointer", out of the type system.
Of course, pointer is not safe, however ATS2 can safely manage the pointer using linear types.
ATS2 does not have "call by reference". Everything is value on ATS2.
The value has own size, however, not have a relationship.
You could make the relationship between values, using type.
The relationship between pointer and value can be understood on "reference", or "at-view" that is linear type pointer.
The programmer can choose it.

Any relationship is not implemented by ATS2 language implementation.
Every relationship is located at the library.

### Hongwei check

I assume that this kind of "philosophical" stuff is always very difficult
to translate.

ATS is a layered system: dynamics: statics: sorts. The statics is meant
to reason about dynamics. Say that you have an array of 0's and 1's. A type
for this array may state that there are equal number of 0's and 1's in
this array at a particular point (though how 0's and 1's are distributed
is unspecified). Your waterpipe analogy is also a good one: shape stays
but content can change.

Say you write a program in Python or Ruby. Once your program is constructed,
what should you do? Most likely, you want to run it so that you may find some bugs.
Then you try to fix the bugs and repeat the process. It is not surprising that such
languages put emphasis on unit testing.

In ATS, you can do the same but there is another option. You can try to refine the
types in your program so that you can flush out some (potential) bugs. What is so
attractive about this option is that you do not have to wait until your program is ready to
run. You can (and probably should) do it while you are developing your program.

So while types themselves are static, types assigned to values can be refined.
Compared to OCaml and Haskell, I think it is probably fair to say that ATS supports
type refinement to a much greater extent.

### John Skaller's comment

> So while types themselves are static, types assigned to values can be refined.
> Compared to OCaml and Haskell, I think it is probably fair to say that ATS supports
> type refinement to a much greater extent.

Although no expert and unsure how one would measure such extent,
I would point out Ocaml polymorphic variants, which I suspect are considerably
higher level than ATS typing.

However, there are problems. Here's a rough description.

Originally, polymorphic variants were flat. A polymorphic variant is just
an arbitrary set of variants (injections, type constructors ...).
Unlike ordinary variants where a union type had fixed variants.

So consider processing some cases A so that after we have
an overlapping set of cases B, with ordinary variants you have
to translate to corresponding but distinct variants, with polymorphic
variants you do not. This provides both run time performance advantage
as well as reducing coding load.

I was one of the first users, trying to use them in my compiler.
Compilers translate terms in many passes and using a fat set
of all possibilities as inputs and output for every pass is common
practice but it is easy to break invariants.

But flat polymorphic variants are of no use here because the terms a compiler
deals with are almost universally recursive.

Enter covariant polymorphic variants.

Consider a type

```ocaml
        type t1 = [ `A of t1 | `B | `C]
```

and suppose you want to get rid of the C. Then you have a type

```ocaml
        type t2 = [`A of t1 | `B ]
```

by throwing out the `C term, which is no good at all because the argument of
the `A constructor is still the old t1. We need to reduce that to t2.

The method for doing this is hard, we have to use open recursion:

```ocaml
        type 'a t2' = [`A of 'a | `B]
        type 'a t1' = ['a t2' | `C]
        type t2 = 'a t2' as 'a
        type t1 = 'a t1' as 'a
```

[I think that's right .. er .. hmm ]

Anyhow the key point is on line 2: we built t1' on top of t2' by replacing
the recursion with a type variable. This makes the terms "flat" but parametric.

Then we close the terms with recursion. so now t1 is a genuine subtype of t2.
We have to ensure covariance here because the processing function that removes
the `C term is recursive.

This is a simple example, which shows it isn't too hard. Very useful indeed
if you have a type with 20 or so variants (which I do in my compiler).

But there's a problem, and it's a killer. There isn't just one type involved,
there are 6 or more mutually recursive types.

So now, you get a combinatorial explosion, you need 6 or more parameters
in the open types and closing them precisely is well nigh impossible.

In the end I gave up and went back to "assert false" on branches that
shouldn't occur. Static checking would be much better but it would
make the code very difficult to get right, and also very fragile.

Furthermore, the usage in explosive/propagating. Lets suppose a term

```ocaml
        Symbol of int * descr | Literal of float
```

is used somewhere and you refine type descr as you process these terms ..
then you have to refine the above type as well. Refinements propagate to all
parents (including self if the type is recursive).

ATS typing is quite different of course and refinement isn't done the same way,
but the issue above with refinement would seem to be a universal issue.

Actually there's another example, well known: take pointer types in C and
throw in "const". That broke almost every program in existence including
pretty much the whole C Standard library. C++ was designed with const
already there but it introduced a lot of complexity. and the
concept really broken down with templates.

Another interesting example is Posix. No one can be happy with the fact
everything is an int: file descriptors, sockets, error codes, thread ids ..
even Posix isn't happy about this and uses typedefs to try to distinguish.
In the Felix bindings for Posix, I can and do use stronger typing,
but always it creates a mess because each function has strange special
cases and overlaps that don't fit any sane typing scheme.

I'm really interested to see how ATS handles these issues. Refinements
have to propagate or they're useless, but not too far or they render the
code too difficult to write and modify. They need to be contained somehow,
for example by hiding them behind an interface (abstraction).
