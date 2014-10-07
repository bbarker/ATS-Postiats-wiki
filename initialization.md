## Arrays
Arrays have the following type
```
@[type][length](initial value(s))
```
For example:
```ocaml
   var A0 = @[int][4]() // A0 = ?,?,?,?
   var A1 = @[int][4](1) // A1 = 1,1,1,1
   var A2 = @[int][4](1,2) // A2 = 1,2,1,2
   var A3 = @[int][4](1,2,3) // A3 = 1,2,3,1
   var A4 = @[int][4](1,2,3,4) // A4 = 1,2,3,4
   var A5 = @[int][4](1,2,3,4,5) // A5 = 1,2,3,4
```

The following example demonstrates how array initialization can be used in more detail:


```ocaml
(* ****** ****** *)
//
#include
"share/atspre_staload.hats"
//
(* ****** ****** *)


staload
UN = "prelude/SATS/unsafe.sats"


fun loop {n: nat} (n: int n, a1p: ptr, a2p: ptr
                           , a3p: ptr, a4p: ptr): void = let
val () = println!($UN.ptr0_get<int>(a1p), " ",
                  $UN.ptr0_get<int>(a2p), " ",
                  $UN.ptr0_get<int>(a3p), " ",
                  $UN.ptr0_get<int>(a4p), "\n")
in
 if n > 1 then loop(n-1, ptr0_succ<int>(a1p), ptr0_succ<int>(a2p),
                         ptr0_succ<int>(a3p), ptr0_succ<int>(a4p))
end // end of loop(...)


implement main0 () = {

val arr_len = 5
var my_array1 = @[int][arr_len](1)
var my_array2 = @[int][arr_len](1,2,3,4)
var my_array3 = @[int][arr_len](1,2,3,4,5)
var my_array4 = @[int][arr_len](1,2,3,4,5,6)

val a1p = addr@(my_array1)
val a2p = addr@(my_array2)
val a3p = addr@(my_array3)
val a4p = addr@(my_array4)

val () = loop(arr_len, a1p, a2p, a3p, a4p)

val x = 5
} // end of main0()
```

Output:
```
$ ./a.exe
1 1 1 1

1 2 2 2

1 3 3 3

1 4 4 4

1 1 5 5
```
