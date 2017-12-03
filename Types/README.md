# Types

A type determines the set of values together with operations and methods specific to those values.\
A type may be denoted by a *type name*, if it has one, or specified using a *type literal*, which composes a type from existing types.

<pre>
<a id="Type">Type</a>      = <a href="#TypeName">TypeName</a> | <a href="#TypeLit">TypeLit</a> | "(" <a href="#Type">Type</a> ")" .
<a id="TypeName">TypeName</a>  = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> | <a href="/Expressions/qualified_identifiers.html#QualifiedIdent">QualifiedIdent</a> .
<a id="TypeLit">TypeLit</a>   = <a href="/Types/array_types.html#ArrayType">ArrayType</a> | <a href="/Types/struct_types.html#StructType">StructType</a> | <a href="/Types/pointer_types.html#PointerType">PointerType</a> | <a href="/Types/function_types.html#FunctionType">FunctionType</a> | <a href="/Types/interface_types.html#InterfaceType">InterfaceType</a> | <a href="/Types/slice_types.html#SliceType">SliceType</a> | <a href="/Types/map_types.html#MapType">MapType</a> | <a href="/Types/channel_types.html#ChannelType">ChannelType</a> .
</pre>

Named instances of the boolean, numeric, and string types are [predeclared](/Declarations%20and%20scope/predeclared_identifiers.html). 
Other named types are introduced with [type declarations](/Declarations%20and%20scope/type_declarations.html).
*Composite types*—array, struct, pointer, function, interface, slice, map, and channel types—may be constructed using type literals.


Each type T has an *underlying type*: If T is one of the predeclared boolean, numeric, or string types, or a type literal, the corresponding underlying type is T itself. Otherwise, T's underlying type is the underlying type of the type to which T refers in its [type declaration](/Declarations%20and%20scope/type_declarations.html).

```
type (
    A1 = string
    A2 = A1
)

type (
    B1 string
    B2 B1
    B3 []B1
    B4 B3
)
```

The underlying type of string, A1, A2, B1 and B2 is string. The underlying type of []B1, B3, and B4 is []B1.