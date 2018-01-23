# Manipulating complex numbers

Three functions assemble and disassemble complex numbers. The built-in function complex constructs a complex value from a floating-point real and imaginary part, while real and imag extract the real and imaginary parts of a complex value.

```go
complex(realPart, imaginaryPart floatT) complexT
real(complexT) floatT
imag(complexT) floatT
```

The type of the arguments and return value correspond. For complex, the two arguments must be of the same floating-point type and the return type is the complex type with the corresponding floating-point constituents: complex64 for float32 arguments, and complex128 for float64 arguments. If one of the arguments evaluates to an untyped constant, it is first [converted](/Expressions/conversions.html) to the type of the other argument. If both arguments evaluate to untyped constants, they must be non-complex numbers or their imaginary parts must be zero, and the return value of the function is an untyped complex constant.

For real and imag, the argument must be of complex type, and the return type is the corresponding floating-point type: float32 for a complex64 argument, and float64 for a complex128 argument. If the argument evaluates to an untyped constant, it must be a number, and the return value of the function is an untyped floating-point constant.

The real and imag functions together form the inverse of complex, so for a value z of a complex type Z, z == Z(complex(real(z), imag(z))).

If the operands of these functions are all constants, the return value is a constant.

```go
var a = complex(2, -2)             // complex128
const b = complex(1.0, -1.4)       // untyped complex constant 1 - 1.4i
x := float32(math.Cos(math.Pi/2))  // float32
var c64 = complex(5, -x)           // complex64
var s uint = complex(1, 0)       // untyped complex constant 1 + 0i can be converted to uint
_ = complex(1, 2<<s)               // illegal: 2 assumes floating-point type, cannot shift
var rl = real(c64)                 // float32
var im = imag(a)                   // float64
const c = imag(b)                  // untyped constant -1.4
_ = imag(3 << s)                   // illegal: 3 assumes complex type, cannot shift
```
