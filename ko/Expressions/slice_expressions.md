# Slice expressions

Slice expressions construct a substring or slice from a string, array, pointer to array, or slice. There are two variants: a simple form that specifies a low and high bound, and a full form that also specifies a bound on the capacity.

## Simple slice expressions

For a string, array, pointer to array, or slice a, the primary expression

```go
a[low : high]
```

constructs a substring or slice. The *indices* low and high select which elements of operand a appear in the result. The result has indices starting at 0 and length equal to `high - low`. After slicing the array a

```go
a := [5]int{1, 2, 3, 4, 5}
s := a[1:4]
```

the slice s has type []int, length 3, capacity 4, and elements

```go
s[0] == 2
s[1] == 3
s[2] == 4
```

For convenience, any of the indices may be omitted. A missing low index defaults to zero; a missing high index defaults to the length of the sliced operand:

```go
a[2:]  // same as a[2 : len(a)]
a[:3]  // same as a[0 : 3]
a[:]   // same as a[0 : len(a)]
```

If a is a pointer to an array, a[low : high] is shorthand for (*a)[low : high].

For arrays or strings, the indices are in range if 0 <= low <= high <= len(a), otherwise they are out of *range*. For slices, the upper index bound is the slice capacity cap(a) rather than the length. A [constant](/Constants/) index must be non-negative and representable by a value of type int; for arrays or constant strings, constant indices must also be in range. If both indices are constant, they must satisfy low <= high. If the indices are out of range at run time, a [run-time panic](/Run-time%20panics/) occurs.

Except for [untyped strings](/Constatns/), if the sliced operand is a string or slice, the result of the slice operation is a non-constant value of the same type as the operand. For untyped string operands the result is a non-constant value of type `string`. If the sliced operand is an array, it must be [addressable](/Expressions/address_operators.html) and the result of the slice operation is a slice with the same element type as the array.

If the sliced operand of a valid slice expression is a `nil` slice, the result is a `nil` slice. Otherwise, the result shares its underlying array with the operand.

## Full slice expressions

For an array, pointer to array, or slice a (but not a string), the primary expression

```go
a[low : high : max]
```

constructs a slice of the same type, and with the same length and elements as the simple slice expression a[low : high]. Additionally, it controls the resulting slice's capacity by setting it to max - low. Only the first index may be omitted; it defaults to 0. After slicing the array a

```go
a := [5]int{1, 2, 3, 4, 5}
t := a[1:3:5]
```

the slice t has type []int, length 2, capacity 4, and elements

```go
t[0] == 2
t[1] == 3
```

As for simple slice expressions, if a is a pointer to an array, a[low : high : max] is shorthand for (*a)[low : high : max]. If the sliced operand is an array, it must be [addressable](/Expressions/address_operators.html).

The indices are in *range* if 0 <= low <= high <= max <= cap(a), otherwise they are out of range. A [constant](/Constants/) index must be non-negative and representable by a value of type int; for arrays, constant indices must also be in range. If multiple indices are constant, the constants that are present must be in range relative to each other. If the indices are out of range at run time, a [run-time panic](/Run-time%20panics/) occurs.
