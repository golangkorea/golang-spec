# [Numeric types](#numeric-types)

A *numeric type* represents sets of integer or floating-point values. The predeclared architecture-independent numeric types are:

    uint8       the set of all unsigned  8-bit integers (0 to 255)
    uint16      the set of all unsigned 16-bit integers (0 to 65535)
    uint32      the set of all unsigned 32-bit integers (0 to 4294967295)
    uint64      the set of all unsigned 64-bit integers (0 to 18446744073709551615)
    
    int8        the set of all signed  8-bit integers (-128 to 127)
    int16       the set of all signed 16-bit integers (-32768 to 32767)
    int32       the set of all signed 32-bit integers (-2147483648 to 2147483647)
    int64       the set of all signed 64-bit integers (-9223372036854775808 to 9223372036854775807)
    
    float32     the set of all IEEE-754 32-bit floating-point numbers
    float64     the set of all IEEE-754 64-bit floating-point numbers
    
    complex64   the set of all complex numbers with float32 real and imaginary parts
    complex128  the set of all complex numbers with float64 real and imaginary parts
    
    byte        alias for uint8
    rune        alias for int32
    

The value of an *n*-bit integer is *n* bits wide and represented using [two's complement arithmetic](http://en.wikipedia.org/wiki/Two's_complement).

There is also a set of predeclared numeric types with implementation-specific sizes:

    uint     either 32 or 64 bits
    int      same size as uint
    uintptr  an unsigned integer large enough to store the uninterpreted bits of a pointer value
    

To avoid portability issues all numeric types are distinct except `byte`, which is an alias for `uint8`, and `rune`, which is an alias for `int32`. Conversions are required when different numeric types are mixed in an expression or assignment. For instance, `int32` and `int` are not the same type even though they may have the same size on a particular architecture.