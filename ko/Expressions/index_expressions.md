# Index expressions

A primary expression of the form

```go
a[x]
```

denotes the element of the array, pointer to array, slice, string or map a indexed by x. The value x is called the *index* or *map key*, respectively. The following rules apply:

If a is not a map:

  * the index x must be of integer type or untyped; it is in range if 0 <= x < len(a), otherwise it is out of range
  * a [constant](/Constants/) index must be non-negative and representable by a value of type int

For a of [array type](/Types/array_types.html) A:

  * a [constant](/Constants/) index must be in range
  * if x is out of range at run time, a [run-time panic](/Run-time%20panics/) occurs
  * a[x] is the array element at index x and the type of a[x] is the element type of A

For a of [pointer](/Types/pointer_types.html) to array type:

  * a[x] is shorthand for (*a)[x]

For a of [slice type](/Types/slice_types.html) S:

  * if x is out of range at run time, a [run-time panic](/Run-time%20panics/) occurs
  * a[x] is the slice element at index x and the type of a[x] is the element type of S

For a of [string type](/Types/string_types.html):

  * a [constant]([constant](/Constants/) index must be in range if the string a is also constant
  * if x is out of range at run time, a [run-time panic](/Run-time%20panics/) occurs
  * a[x] is the non-constant byte value at index x and the type of a[x] is byte
  * a[x] may not be assigned to

For a of [map type](/Types/map_types.html) M:

  * x's type must be assignable to the key type of M
  * if the map contains an entry with key x, a[x] is the map value with key x and the type of a[x] is the value type of M
  * if the map is nil or does not contain such an entry, a[x] is the zero value for the value type of M

Otherwise a[x] is illegal.

An index expression on a map a of type map[K]V used in an [assignment](/Properties%20of%20types%20and%20values/assignability.html) or initialization of the special form

```go
v, ok = a[x]
v, ok := a[x]
var v, ok = a[x]
```

yields an additional untyped boolean value. The value of ok is true if the key x is present in the map, and false otherwise.

Assigning to an element of a nil map causes a [run-time panic](/Run-time%20panics/).
