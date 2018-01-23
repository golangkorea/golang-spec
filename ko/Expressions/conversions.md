# Conversions

Conversions are expressions of the form T(x) where T is a type and x is an expression that can be converted to type T.

<pre>
<a id="Conversion">Conversion</a> = <a href="/Types/#Type">Type</a> "(" <a href="/Expressions/operators.html#Expression">Expression</a> [ "," ] ")" .
</pre>

If the type starts with the operator * or <-, or if the type starts with the keyword func and has no result list, it must be parenthesized when necessary to avoid ambiguity:

```go
*Point(p)        // same as *(Point(p))
(*Point)(p)      // p is converted to *Point
<-chan int(c)    // same as <-(chan int(c))
(<-chan int)(c)  // c is converted to <-chan int
func()(x)        // function signature func() x
(func())(x)      // x is converted to func()
(func() int)(x)  // x is converted to func() int
func() int(x)    // x is converted to func() int (unambiguous)
```

A [constant](/Constants/) value x can be converted to type T in any of these cases:

  * x is representable by a value of type T.
  * x is a floating-point constant, T is a floating-point type, and x is representable by a value of type T after rounding using IEEE 754 round-to-even rules, but with an IEEE -0.0 further rounded to an unsigned 0.0. The constant T(x) is the rounded value.
  * x is an integer constant and T is a [string type](/Types/string_types.html). The [same rule](#conversions-to-and-from-a-string-type) as for non-constant x applies in this case.

Converting a constant yields a typed constant as result.

```go
uint(iota)               // iota value of type uint
float32(2.718281828)     // 2.718281828 of type float32
complex128(1)            // 1.0 + 0.0i of type complex128
float32(0.49999999)      // 0.5 of type float32
float64(-1e-1000)        // 0.0 of type float64
string('x')              // "x" of type string
string(0x266c)           // "♬" of type string
MyString("foo" + "bar")  // "foobar" of type MyString
string([]byte{'a'})      // not a constant: []byte{'a'} is not a constant
(*int)(nil)              // not a constant: nil is not a constant, *int is not a boolean, numeric, or string type
int(1.2)                 // illegal: 1.2 cannot be represented as an int
string(65.0)             // illegal: 65.0 is not an integer constant
```

A non-constant value x can be converted to type T in any of these cases:

  * x is [assignable](/Properties%20of%20types%20and%20values/assignability.html) to T.
  * ignoring struct tags (see below), x's type and T have [identical](#Type_identity) [underlying types](#Types).
  * ignoring struct tags (see below), x's type and T are pointer types that are not [defined types](/Declarations%20and%20scope/type_declarations.html#type-definitions), and their pointer base types have identical underlying types.
  * x's type and T are both integer or floating point types.
  * x's type and T are both complex types.
  * x is an integer or a slice of bytes or runes and T is a string type.
  * x is a string and T is a slice of bytes or runes.

[Struct tags](/Struct_types/) are ignored when comparing struct types for identity for the purpose of conversion:

```go
type Person struct {
    Name    string
    Address *struct {
        Street string
        City   string
    }
}

var data *struct {
    Name    string `json:"name"`
    Address *struct {
        Street string `json:"street"`
        City   string `json:"city"`
    } `json:"address"`
}

var person = (*Person)(data)  // ignoring tags, the underlying types are identical
```

Specific rules apply to (non-constant) conversions between numeric types or to and from a string type. These conversions may change the representation of x and incur a run-time cost. All other conversions only change the type but not the representation of x.

There is no linguistic mechanism to convert between pointers and integers. The package [unsafe](/System%20considerations/package_unsafe.html) implements this functionality under restricted circumstances.

## Conversions between numeric types

For the conversion of non-constant numeric values, the following rules apply:

  1. When converting between integer types, if the value is a signed integer, it is sign extended to implicit infinite precision; otherwise it is zero extended. It is then truncated to fit in the result type's size. For example, if v := uint16(0x10F0), then uint32(int8(v)) == 0xFFFFFFF0. The conversion always yields a valid value; there is no indication of overflow.
  2. When converting a floating-point number to an integer, the fraction is discarded (truncation towards zero).
  3. When converting an integer or floating-point number to a floating-point type, or a complex number to another complex type, the result value is rounded to the precision specified by the destination type. For instance, the value of a variable x of type float32 may be stored using additional precision beyond that of an IEEE-754 32-bit number, but float32(x) represents the result of rounding x's value to 32-bit precision. Similarly, x + 0.1 may use more than 32 bits of precision, but float32(x + 0.1) does not.

In all non-constant conversions involving floating-point or complex values, if the result type cannot represent the value the conversion succeeds but the result value is implementation-dependent.

## Conversions to and from a string type

  1. Converting a signed or unsigned integer value to a string type yields a string containing the UTF-8 representation of the integer. Values outside the range of valid Unicode code points are converted to "\uFFFD".
<pre>
string('a')       // "a"
string(-1)        // "\ufffd" == "\xef\xbf\xbd"
string(0xf8)      // "\u00f8" == "ø" == "\xc3\xb8"
type MyString string
MyString(0x65e5)  // "\u65e5" == "日" == "\xe6\x97\xa5"
</pre>
  2. Converting a slice of bytes to a string type yields a string whose successive bytes are the elements of the slice.
<pre>
string([]byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'})   // "hellø"
string([]byte{})                                     // ""
string([]byte(nil))                                  // ""
&nbsp;
type MyBytes []byte
string(MyBytes{'h', 'e', 'l', 'l', '\xc3', '\xb8'})  // "hellø"
</pre>
  3. Converting a slice of runes to a string type yields a string that is the concatenation of the individual rune values converted to strings.
<pre>
string([]rune{0x767d, 0x9d6c, 0x7fd4})   // "\u767d\u9d6c\u7fd4" == "白鵬翔"
string([]rune{})                         // ""
string([]rune(nil))                      // ""
&nbsp;
type MyRunes []rune
string(MyRunes{0x767d, 0x9d6c, 0x7fd4})  // "\u767d\u9d6c\u7fd4" == "白鵬翔"
</pre>
  4. Converting a value of a string type to a slice of bytes type yields a slice whose successive elements are the bytes of the string.
<pre>
[]byte("hellø")   // []byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'}
[]byte("")        // []byte{}
&nbsp;
MyBytes("hellø")  // []byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'}
</pre>
  5. Converting a value of a string type to a slice of runes type yields a slice containing the individual Unicode code points of the string.
<pre>
[]rune(MyString("白鵬翔"))  // []rune{0x767d, 0x9d6c, 0x7fd4}
[]rune("")                 // []rune{}
&nbsp;
MyRunes("白鵬翔")           // []rune{0x767d, 0x9d6c, 0x7fd4}
</pre>