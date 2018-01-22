# Appending to and copying slices

The built-in functions append and copy assist in common slice operations. For both functions, the result is independent of whether the memory referenced by the arguments overlaps.

The [variadic](/Types/function_types.html) function append appends zero or more values x to s of type S, which must be a slice type, and returns the resulting slice, also of type S. The values x are passed to a parameter of type ...T where T is the [element type](/Types/slice_types.html) of S and the respective [parameter passing rules](/Expressions/passing_arguments_to__parameters.html) apply. As a special case, append also accepts a first argument assignable to type []byte with a second argument of string type followed by .... This form appends the bytes of the string.

```go
append(s S, x ...T) S  // T is the element type of S
```

If the capacity of s is not large enough to fit the additional values, append allocates a new, sufficiently large underlying array that fits both the existing slice elements and the additional values. Otherwise, append re-uses the underlying array.

```go
s0 := []int{0, 0}
s1 := append(s0, 2)                // append a single element     s1 == []int{0, 0, 2}
s2 := append(s1, 3, 5, 7)          // append multiple elements    s2 == []int{0, 0, 2, 3, 5, 7}
s3 := append(s2, s0...)            // append a slice              s3 == []int{0, 0, 2, 3, 5, 7, 0, 0}
s4 := append(s3[3:6], s3[2:]...)   // append overlapping slice    s4 == []int{3, 5, 7, 2, 3, 5, 7, 0, 0}

var t []interface{}
t = append(t, 42, 3.1415, "foo")   //                             t == []interface{}{42, 3.1415, "foo"}

var b []byte
b = append(b, "bar"...)            // append string contents      b == []byte{'b', 'a', 'r' }
```

The function copy copies slice elements from a source src to a destination dst and returns the number of elements copied. Both arguments must have [identical](/Properties%20of%20types%20and%20values/type_identity.html) element type T and must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to a slice of type []T. The number of elements copied is the minimum of len(src) and len(dst). As a special case, copy also accepts a destination argument assignable to type []byte with a source argument of a string type. This form copies the bytes from the string into the byte slice.

```go
copy(dst, src []T) int
copy(dst []byte, src string) int
```

Examples:

```go
var a = [...]int{0, 1, 2, 3, 4, 5, 6, 7}
var s = make([]int, 6)
var b = make([]byte, 5)
n1 := copy(s, a[0:])            // n1 == 6, s == []int{0, 1, 2, 3, 4, 5}
n2 := copy(s, s[2:])            // n2 == 4, s == []int{2, 3, 4, 5, 4, 5}
n3 := copy(b, "Hello, World!")  // n3 == 5, b == []byte("Hello")
```
