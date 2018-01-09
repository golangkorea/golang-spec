# Method expressions

If M is in the [method set](/Types/method_sets.html) of type T, T.M is a function that is callable as a regular function with the same arguments as M prefixed by an additional argument that is the receiver of the method.

<pre>
<a id="MethodExpr">MethodExpr</a>    = <a href="#ReceiverType">ReceiverType</a> "." <a href="/Types/interface_types.html#MethodName">MethodName</a> .
<a id="ReceiverType">ReceiverType</a>  = <a href="/Types/#TypeName">TypeName</a> | "(" "*" <a href="/Types/#TypeName">TypeName</a> ")" | "(" <a href="#ReceiverType">ReceiverType</a> ")" .
</pre>

Consider a struct type T with two methods, Mv, whose receiver is of type T, and Mp, whose receiver is of type *T.

```go
type T struct {
    a int
}
func (tv  T) Mv(a int) int         { return 0 }  // value receiver
func (tp *T) Mp(f float32) float32 { return 1 }  // pointer receiver

var t T
```

The expression

```go
T.Mv
```

yields a function equivalent to Mv but with an explicit receiver as its first argument; it has signature

```go
func(tv T, a int) int
```

That function may be called normally with an explicit receiver, so these five invocations are equivalent:

```go
t.Mv(7)
T.Mv(t, 7)
(T).Mv(t, 7)
f1 := T.Mv; f1(t, 7)
f2 := (T).Mv; f2(t, 7)
```

Similarly, the expression

(*T).Mp yields a function value representing Mp with signature

func(tp *T, f float32) float32 For a method with a value receiver, one can derive a function with an explicit pointer receiver, so

```go
(*T).Mv
```

yields a function value representing Mv with signature

```go
func(tv *T, a int) int
```

Such a function indirects through the receiver to create a value to pass as the receiver to the underlying method; the method does not overwrite the value whose address is passed in the function call.

The final case, a value-receiver function for a pointer-receiver method, is illegal because pointer-receiver methods are not in the method set of the value type.

Function values derived from methods are called with function call syntax; the receiver is provided as the first argument to the call. That is, given f := T.Mv, f is invoked as f(t, 7) not t.f(7). To construct a function that binds the receiver, use a [function literal](/Expressions/function_literals.html) or [method value](/Expressions/method_values.html).

It is legal to derive a function value from a method of an interface type. The resulting function takes an explicit receiver of that interface type.