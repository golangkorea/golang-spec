# Composite literals

Composite literals construct values for structs, arrays, slices, and maps and create a new value each time they are evaluated. They consist of the type of the literal followed by a brace-bound list of elements. Each element may optionally be preceded by a corresponding key.

<pre>
<a id="CompositeLit">CompositeLit</a>  = <a href="#LiteralType">LiteralType</a> <a href="#LiteralValue">LiteralValue</a> .
<a id="LiteralType">LiteralType</a>   = <a href="/Types/struct_types.html#StructType">StructType</a> | <a href="/Types/array_types.html#ArrayType">ArrayType</a> | "[" "..." "]" <a href="/Types/array_types.html#ElementType">ElementType</a> | <a href="/Types/slice_types.html#SliceType">SliceType</a> | <a href="/Types/map_types.html#MapType">MapType</a> | <a href="/Types/#TypeName">TypeName</a> .
<a id="LiteralValue">LiteralValue</a>  = "{" [ <a href="#ElementList">ElementList</a> [ "," ] ] "}" .
<a id="ElementList">ElementList</a>   = <a href="#KeyedElement">KeyedElement</a> { "," <a href="#KeyedElement">KeyedElement</a> } .
<a id="KeyedElement">KeyedElement</a>  = [ <a href="#Key">Key</a> ":" ] <a href="#Element">Element</a> .
<a id="Key">Key</a>           = <a href="#FieldName">FieldName</a> | <a href="/Expressions/operators.html#Expression">Expression</a> | <a href="#LiteralValue">LiteralValue</a> .
<a id="FieldName">FieldName</a>     = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
<a id="Element">Element</a>       = <a href="/Expressions/operators.html#Expression">Expression</a> | <a href="#LiteralValue">LiteralValue</a> .
</pre>

The LiteralType's underlying type must be a struct, array, slice, or map type (the grammar enforces this constraint except when the type is given as a TypeName). The types of the elements and keys must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to the respective field, element, and key types of the literal type; there is no additional conversion. The key is interpreted as a field name for struct literals, an index for array and slice literals, and a key for map literals. For map literals, all elements must have a key. It is an error to specify multiple elements with the same field name or constant key value. For non-constant map keys, see the section on [evaluation order](/Expressions/order_of_evaluation.html).

For struct literals the following rules apply:

- A key must be a field name declared in the struct type.
- An element list that does not contain any keys must list an element for each struct field in the order in which the fields are declared.
- If any element has a key, every element must have a key.
- An element list that contains keys does not need to have an element for each struct field. Omitted fields get the zero value for that field.
- A literal may omit the element list; such a literal evaluates to the zero value for its type.
- It is an error to specify an element for a non-exported field of a struct belonging to a different package.

Given the declarations

```go
type Point3D struct { x, y, z float64 }
type Line struct { p, q Point3D }
```

one may write

```golang
origin := Point3D{}                            // zero value for Point3D
line := Line{origin, Point3D{y: -4, z: 12.3}}  // zero value for line.q.x
```

For array and slice literals the following rules apply:

- Each element has an associated integer index marking its position in the array.
- An element with a key uses the key as its index. The key must be a non-negative constant representable by a value of type `int`; and if it is typed it must be of integer type.
- An element without a key uses the previous element's index plus one. If the first element has no key, its index is zero.

[Taking the address](/Expressions/address_operators.html) of a composite literal generates a pointer to a unique [variable](/Variables/) initialized with the literal's value.

    var pointer *Point3D = &Point3D{y: 1000}
    

The length of an array literal is the length specified in the literal type. If fewer elements than the length are provided in the literal, the missing elements are set to the zero value for the array element type. It is an error to provide elements with index values outside the index range of the array. The notation ... specifies an array length equal to the maximum element index plus one.

    buffer := [10]string{}             // len(buffer) == 10
    intSet := [6]int{1, 2, 3, 5}       // len(intSet) == 6
    days := [...]string{"Sat", "Sun"}  // len(days) == 2
    

A slice literal describes the entire underlying array literal. Thus, the length and capacity of a slice literal are the maximum element index plus one. A slice literal has the form

    []T{x1, x2, … xn}
    

and is shorthand for a slice operation applied to an array:

    tmp := [n]T{x1, x2, … xn}
    tmp[0 : n]
    

Within a composite literal of array, slice, or map type T, elements or map keys that are themselves composite literals may elide the respective literal type if it is identical to the element or key type of T. Similarly, elements or keys that are addresses of composite literals may elide the &T when the element or key type is *T.

    [...]Point{{1.5, -3.5}, {0, 0}}     // same as [...]Point{Point{1.5, -3.5}, Point{0, 0}}
    [][]int{{1, 2, 3}, {4, 5}}          // same as [][]int{[]int{1, 2, 3}, []int{4, 5}}
    [][]Point{{{0, 1}, {1, 2}}}         // same as [][]Point{[]Point{Point{0, 1}, Point{1, 2}}}
    map[string]Point{"orig": {0, 0}}    // same as map[string]Point{"orig": Point{0, 0}}
    map[Point]string{{0, 0}: "orig"}    // same as map[Point]string{Point{0, 0}: "orig"}
    
    type PPoint *Point
    [2]*Point{{1.5, -3.5}, {}}          // same as [2]*Point{&Point{1.5, -3.5}, &Point{}}
    [2]PPoint{{1.5, -3.5}, {}}          // same as [2]PPoint{PPoint(&Point{1.5, -3.5}), PPoint(&Point{})}
    

A parsing ambiguity arises when a composite literal using the TypeName form of the LiteralType appears as an operand between the [keyword](/Lexical%20elements/keywords.html) and the opening brace of the block of an "if", "for", or "switch" statement, and the composite literal is not enclosed in parentheses, square brackets, or curly braces. In this rare case, the opening brace of the literal is erroneously parsed as the one introducing the block of statements. To resolve the ambiguity, the composite literal must appear within parentheses.

    if x == (T{a,b,c}[i]) { … }
    if (x == T{a,b,c}[i]) { … }
    

Examples of valid array, slice, and map literals:

    // list of prime numbers
    primes := []int{2, 3, 5, 7, 9, 2147483647}
    
    // vowels[ch] is true if ch is a vowel
    vowels := [128]bool{'a': true, 'e': true, 'i': true, 'o': true, 'u': true, 'y': true}
    
    // the array [10]float32{-1, 0, 0, 0, -0.1, -0.1, 0, 0, 0, -1}
    filter := [10]float32{-1, 4: -0.1, -0.1, 9: -1}
    
    // frequencies in Hz for equal-tempered scale (A4 = 440Hz)
    noteFrequency := map[string]float32{
        "C0": 16.35, "D0": 18.35, "E0": 20.60, "F0": 21.83,
        "G0": 24.50, "A0": 27.50, "B0": 30.87,
    }