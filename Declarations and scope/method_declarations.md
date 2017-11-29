# Method declarations

A method is a [function](/Declarations%20and%20scope/function_declarations.html) with a *receiver*. A method declaration binds an identifier, the *method name*, to a method, and associates the method with the receiver's *base type*.

<pre>
<a id="MethodDecl">MethodDecl</a>   = "func" <a href="#Receiver">Receiver</a> <a href="/Types/interface_types.html#MethodName">MethodName</a> ( <a href="/Declarations%20and%20scope/function_declarations.html#Function">Function</a> | <a href="/Types/function_types.html#Signature">Signature</a> ) .
<a id="Receiver">Receiver</a>     = <a href="/Types/function_types.html#Parameters">Parameters</a> .
</pre>

The receiver is specified via an extra parameter section preceding the method name. That parameter section must declare a single non-variadic parameter, the receiver. Its type must be of the form T or *T (possibly using parentheses) where T is a type name. The type denoted by T is called the receiver *base type*; it must not be a pointer or interface type and it must be declared in the same package as the method. The method is said to be bound to the base type and the method name is visible only within [selectors](/Expressions/selectors.html) for type T or *T.

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

# Alias declarations

An alias declaration binds an identifier, the _alias_ , to a [constant](#Constant_declarations), [type](#Type_declarations), [variable](#Variable_declarations), or [function](#Function_declarations) denoted by a [qualified identifier](#Qualified_identifiers) and declared in a different package.

<pre>
<a id="AliasSpec">AliasSpec</a> = identifier "=>" <a href="#QualifiedIdent">QualifiedIdent</a> .
</pre>

The effect of referring to a constant, type, variable, or function by an alias is indistinguishable from referring to it by its original name. For example, the type denoted by a type alias and the aliased type are [identical](#Type_identity).

An alias declaration may appear only as a form of constant, type, variable, or function declaration at the package level, and the aliased entity must be a constant, type, variable, or function respectively. Alias declarations inside functions are not permitted.

```
const (
	G  =  6.67408e-11      // regular and alias declarations may be grouped
	Pi => math.Pi          // same effect as: Pi = math.Pi
)

type Struct => types.Struct    // re-export of types.Struct

func sin => math.Sin           // non-exported shortcut for frequently used function
```

An alias declaration may not refer to package [unsafe](#Package_unsafe).