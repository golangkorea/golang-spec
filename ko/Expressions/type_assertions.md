# Type assertions

For an expression x of [interface type](/Types/interface_types.html) and a type T, the primary expression

```go
x.(T)
```

asserts that x is not nil and that the value stored in x is of type T. The notation x.(T) is called a *type assertion*.

More precisely, if T is not an interface type, x.(T) asserts that the dynamic type of x is [identical](/Properties%20of%20types%20and%20values/type_identity.html) to the type T. In this case, T must [implement](/Types/method_sets.html) the (interface) type of x; otherwise the type assertion is invalid since it is not possible for x to store a value of type T. If T is an interface type, x.(T) asserts that the dynamic type of x implements the interface T.

If the type assertion holds, the value of the expression is the value stored in x and its type is T. If the type assertion is false, a [run-time panic](/Run-time%20panics/) occurs. In other words, even though the dynamic type of x is known only at run time, the type of x.(T) is known to be T in a correct program.

```go
var x interface{} = 7          // x has dynamic type int and value 7
i := x.(int)                   // i has type int and value 7

type I interface { m() }

func f(y I) {
    s := y.(string)        // illegal: string does not implement I (missing method m)
    r := y.(io.Reader)     // r has type io.Reader and the dynamic type of y must implement both I and io.Reader
    …
}
```

A type assertion used in an [assignment](/Statements/assignments.html) or initialization of the special form

```go
v, ok = x.(T)
v, ok := x.(T)
var v, ok = x.(T)
```

yields an additional untyped boolean value. The value of ok is true if the assertion holds. Otherwise it is false and the value of v is the [zero value](/Program%20initialization%20and%20execution/the_zero_value.html) for type T. No run-time panic occurs in this case.
