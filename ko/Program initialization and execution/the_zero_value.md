# [The zero value](#the-zero-value)

When storage is allocated for a [variable](/Variables/), either through a declaration or a call of `new`, or when a new value is created, either through a composite literal or a call of `make`, and no explicit initialization is provided, the variable or value is given a default value. Each element of such a variable or value is set to the *zero value* for its type: `false` for booleans, 0 for integers, 0.0 for floats, "" for strings, and `nil` for pointers, functions, interfaces, slices, channels, and maps. This initialization is done recursively, so for instance each element of an array of structs will have its fields zeroed if no value is specified.

These two simple declarations are equivalent:

    var i int
    var i int = 0
    

After

    type T struct { i int; f float64; next *T }
    t := new(T)
    

the following holds:

    t.i == 0
    t.f == 0.0
    t.next == nil
    

The same would also be true after

    var t T