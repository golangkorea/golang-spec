# Struct types

A struct is a sequence of named elements, called fields, each of which has a name and a type. Field names may be specified explicitly (IdentifierList) or implicitly (AnonymousField). Within a struct, non-[blank](/Declarations%20and%20scope/blank_identifier.html) field names must be [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html).

<pre>
<a id="StructType">StructType</a>     = "struct" "{" { <a href="#FieldDecl">FieldDecl</a> ";" } "}" .
<a id="FieldDecl">FieldDecl</a>      = (<a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> Type | AnonymousField) [ Tag ] .
<a id="AnonymousField">AnonymousField</a> = [ "*" ] TypeName .
<a id="Tag">Tag</a>            = string_lit .
</pre>

```
// An empty struct.
struct {}

// A struct with 6 fields.
struct {
	x, y int
	u float32
	_ float32  // padding
	A *[]int
	F func()
}
```

A field declared with a type but no explicit field name is an anonymous field, also called an embedded field or an embedding of the type in the struct. An embedded type must be specified as a type name T or as a pointer to a non-interface type name *T, and T itself may not be a pointer type. The unqualified type name acts as the field name.

```
// A struct with four anonymous fields of type T1, *T2, P.T3 and *P.T4
struct {
	T1        // field name is T1
	*T2       // field name is T2
	P.T3      // field name is T3
	*P.T4     // field name is T4
	x, y int  // field names are x and y
}
```

The following declaration is illegal because field names must be unique in a struct type:

```
struct {
	T     // conflicts with anonymous field *T and *P.T
	*T    // conflicts with anonymous field T and *P.T
	*P.T  // conflicts with anonymous field T and *T
}
```

A field or method f of an anonymous field in a struct x is called promoted if x.f is a legal selector that denotes that field or method f.

Promoted fields act like ordinary fields of a struct except that they cannot be used as field names in composite literals of the struct.

Given a struct type S and a type named T, promoted methods are included in the method set of the struct as follows:

If S contains an anonymous field T, the method sets of S and *S both include promoted methods with receiver T. The method set of *S also includes promoted methods with receiver *T.
If S contains an anonymous field *T, the method sets of S and *S both include promoted methods with receiver T or *T.
A field declaration may be followed by an optional string literal tag, which becomes an attribute for all the fields in the corresponding field declaration. An empty tag string is equivalent to an absent tag. The tags are made visible through a reflection interface and take part in type identity for structs but are otherwise ignored.

```
struct {
	x, y float64 ""  // an empty tag string is like an absent tag
	name string  "any string is permitted as a tag"
	_    [4]byte "ceci n'est pas un champ de structure"
}

// A struct corresponding to a TimeStamp protocol buffer.
// The tag strings define the protocol buffer field numbers;
// they follow the convention outlined by the reflect package.
struct {
	microsec  uint64 `protobuf:"1"`
	serverIP6 uint64 `protobuf:"2"`
}
```