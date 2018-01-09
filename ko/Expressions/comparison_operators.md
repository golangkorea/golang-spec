# [Comparison operators](#comparison-operators)

Comparison operators compare two operands and yield an untyped boolean value.

```go
==    equal
!=    not equal
<     less
<=    less or equal
>     greater
>=    greater or equal
```

In any comparison, the first operand must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to the type of the second operand, or vice versa.

The equality operators == and != apply to operands that are *comparable*. The ordering operators <, <=, >, and >= apply to operands that are *ordered*. These terms and the result of the comparisons are defined as follows:

- Boolean values are comparable. Two boolean values are equal if they are either both true or both false.
- Integer values are comparable and ordered, in the usual way.
- Floating point values are comparable and ordered, as defined by the IEEE-754 standard.
- Complex values are comparable. Two complex values u and v are equal if both real(u) == real(v) and imag(u) == imag(v).
- String values are comparable and ordered, lexically byte-wise.
- Pointer values are comparable. Two pointer values are equal if they point to the same variable or if both have value nil. Pointers to distinct [zero-size](/System%20considerations/size_and_alignment_guarantees.html) variables may or may not be equal.
- Channel values are comparable. Two channel values are equal if they were created by the same call to [make](/making_slices,_maps_and_channels.html) or if both have value `nil`.
- Interface values are comparable. Two interface values are equal if they have [identical](/Properties%20of%20types%20and%20values/type_identity.html) dynamic types and equal dynamic values or if both have value nil.
- A value `x` of non-interface type `X` and a value `t` of interface type `T` are comparable when values of type `X` are comparable and `X` implements `T`. They are equal if `t`'s dynamic type is identical to `X` and `t`'s dynamic value is equal to `x`.
- Struct values are comparable if all their fields are comparable. Two struct values are equal if their corresponding non-[blank](/Declarations%20and%20scope/blank_identifier.html) fields are equal.
- Array values are comparable if values of the array element type are comparable. Two array values are equal if their corresponding elements are equal.

A comparison of two interface values with identical dynamic types causes a [run-time panic](/Run-time%20panics/) if values of that type are not comparable. This behavior applies not only to direct interface value comparisons but also when comparing arrays of interface values or structs with interface-valued fields.

Slice, map, and function values are not comparable. However, as a special case, a slice, map, or function value may be compared to the predeclared identifier nil. Comparison of pointer, channel, and interface values to nil is also allowed and follows from the general rules above.

```go
const c = 3 < 4            // c is the untyped boolean constant true

type MyBool bool
var x, y int
var (
    // The result of a comparison is an untyped boolean.
    // The usual assignment rules apply.
    b3        = x == y // b3 has type bool
    b4 bool   = x == y // b4 has type bool
    b5 MyBool = x == y // b5 has type MyBool
)
```