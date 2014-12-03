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