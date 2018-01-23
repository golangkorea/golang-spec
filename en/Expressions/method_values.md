# Method values

If the expression x has static type T and M is in the [method set](/Types/method_sets.html) of type T, x.M is called a *method value*. The method value x.M is a function value that is callable with the same arguments as a method call of x.M. The expression x is evaluated and saved during the evaluation of the method value; the saved copy is then used as the receiver in any calls, which may be executed later.

The type T may be an interface or non-interface type.

As in the discussion of [method expressions](/Expressions/method_expressions.html) above, consider a struct type T with two methods, Mv, whose receiver is of type T, and Mp, whose receiver is of type *T.

```go
type T struct {
	a int
}
func (tv  T) Mv(a int) int         { return 0 }  // value receiver
func (tp *T) Mp(f float32) float32 { return 1 }  // pointer receiver

var t T
var pt *T
func makeT() T
```

The expression

```go
t.Mv
```

yields a function value of type

```go
func(int) int
```

These two invocations are equivalent:

```go
t.Mv(7)
f := t.Mv; f(7)
```

Similarly, the expression

```go
pt.Mp
```

yields a function value of type

```go
func(float32) float32
```

As with [selectors](/Expressions/selectors.html), a reference to a non-interface method with a value receiver using a pointer will automatically dereference that pointer: pt.Mv is equivalent to (*pt).Mv.

As with [method calls](/Expressions/calls.html), a reference to a non-interface method with a pointer receiver using an addressable value will automatically take the address of that value: t.Mp is equivalent to (&t).Mp.

```go
f := t.Mv; f(7)   // like t.Mv(7)
f := pt.Mp; f(7)  // like pt.Mp(7)
f := pt.Mv; f(7)  // like (*pt).Mv(7)
f := t.Mp; f(7)   // like (&t).Mp(7)
f := makeT().Mp   // invalid: result of makeT() is not addressable
```

Although the examples above use non-interface types, it is also legal to create a method value from a value of interface type.

```go
var i interface { M(int) } = myVal
f := i.M; f(7)  // like i.M(7)
```