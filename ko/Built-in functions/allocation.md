# [할당](#allocation)

The built-in function `new` takes a type `T`, allocates storage for a [variable](/Variables/) of that type at run time, and returns a value of type `*T` [pointing](/Types/pointer_types.html) to it. The variable is initialized as described in the section on [initial values](/Program initialization and execution/the_zero_value.html).

```golng
new(T)
```

For instance

```golang
type S struct { a int; b float64 }
new(S)
```

allocates storage for a variable of type `S`, initializes it (`a=0`, `b=0.0`), and returns a value of type `*S` containing the address of the location.