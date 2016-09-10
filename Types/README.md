# Types

A type determines the set of values and operations specific to values of that type. Types may be *named* or *unnamed*. Named types are specified by a (possibly [qualified](/Expressions/qualified_identifiers.html)) [type name](/Declarations%20and%20scope/type_declarations.html); unnamed types are specified using a *type literal*, which composes a new type from existing types.

<pre>
<a id="Type">Type</a>      = <a href="#TypeName">TypeName</a> | <a href="#TypeLit">TypeLit</a> | "(" <a href="#Type">Type</a> ")" .
<a id="TypeName">TypeName</a>  = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> | <a href="/Expressions/qualified_identifiers.html#QualifiedIdent">QualifiedIdent</a> .
<a id="TypeLit">TypeLit</a>   = <a href="/Types/array_types.html#ArrayType">ArrayType</a> | <a href="/Types/struct_types.html#StructType">StructType</a> | <a href="/Types/pointer_types.html#PointerType">PointerType</a> | <a href="/Types/function_types.html#FunctionType">FunctionType</a> | <a href="/Types/interface_types.html#InterfaceType">InterfaceType</a> | <a href="/Types/slice_types.html#SliceType">SliceType</a> | <a href="/Types/map_types.html#MapType">MapType</a> | <a href="/Types/channel_types.html#ChannelType">ChannelType</a> .
</pre>

Named instances of the boolean, numeric, and string types are [predeclared](/Declarations%20and%20scope/predeclared_identifiers.html). *Composite types*—array, struct, pointer, function, interface, slice, map, and channel types—may be constructed using type literals.


Each type T has an *underlying type*: If T is one of the predeclared boolean, numeric, or string types, or a type literal, the corresponding underlying type is T itself. Otherwise, T's underlying type is the underlying type of the type to which T refers in its [type declaration](/Declarations%20and%20scope/type_declarations.html).

```
   type T1 string
   type T2 T1
   type T3 []T1
   type T4 T3
```

The underlying type of string, T1, and T2 is string. The underlying type of []T1, T3, and T4 is []T1.