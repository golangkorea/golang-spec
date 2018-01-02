# Method declarations

A method is a [function](/Declarations%20and%20scope/function_declarations.html) with a *receiver*. A method declaration binds an identifier, the *method name*, to a method, and associates the method with the receiver's *base type*.

<pre>
<a id="MethodDecl">MethodDecl</a> = "func" <a href="#Receiver">Receiver</a> <a href="/Types/interface_types.html#MethodName">MethodName</a> ( <a href="/Declarations%20and%20scope/function_declarations.html#Function">Function</a> | <a href="/Types/function_types.html#Signature">Signature</a> ) .
<a id="Receiver">Receiver</a>   = <a href="/Types/function_types.html#Parameters">Parameters</a> .
</pre>

The receiver is specified via an extra parameter section preceding the method name. That parameter section must declare a single non-variadic parameter, the receiver. Its type must be of the form T or `*T` (possibly using parentheses) where T is a type name. The type denoted by T is called the receiver *base type*; it must not be a pointer or interface type and it must be [declared](/Declarations%20and%20scope/type_declarations.html) in the same package as the method. The method is said to be bound to the base type and the method name is visible only within [selectors](/Expressions/selectors.html) for type T or *T.

A non-[blank](/Declarations%20and%20scope/blank_identifier.html) receiver identifier must be [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html) in the method signature. If the receiver's value is not referenced inside the body of the method, its identifier may be omitted in the declaration. The same applies in general to parameters of functions and methods.

For a base type, the non-blank names of methods bound to it must be unique. If the base type is a [struct type](/Types/struct_types.html), the non-blank method and field names must be distinct.

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

bind the methods `Length` and `Scale`, with receiver type `*Point`, to the base type `Point`.

The type of a method is the type of a function with the receiver as first argument. For instance, the method Scale has type

```
func(p *Point, factor float64)
```

However, a function declared this way is not a method.