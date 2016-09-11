# Method declarations

A method is a function with a receiver. A method declaration binds an identifier, the method name, to a method, and associates the method with the receiver's base type.

<pre>
MethodDecl   = "func" Receiver MethodName ( Function | Signature ) .
Receiver     = Parameters .
</pre>

The receiver is specified via an extra parameter section preceding the method name. That parameter section must declare a single non-variadic parameter, the receiver. Its type must be of the form T or *T (possibly using parentheses) where T is a type name. The type denoted by T is called the receiver base type; it must not be a pointer or interface type and it must be declared in the same package as the method. The method is said to be bound to the base type and the method name is visible only within selectors for type T or *T.

A non-blank receiver identifier must be unique in the method signature. If the receiver's value is not referenced inside the body of the method, its identifier may be omitted in the declaration. The same applies in general to parameters of functions and methods.

For a base type, the non-blank names of methods bound to it must be unique. If the base type is a struct type, the non-blank method and field names must be distinct.

Given type Point, the declarations

```
func (p *Point) Length() float64 {
	return math.Sqrt(p.x * p.x + p.y * p.y)
}

func (p *Point) Scale(factor float64) {
	p.x *= factor
	p.y *= factor
}
```

bind the methods Length and Scale, with receiver type *Point, to the base type Point.

The type of a method is the type of a function with the receiver as first argument. For instance, the method Scale has type

```
func(p *Point, factor float64)
```

However, a function declared this way is not a method.