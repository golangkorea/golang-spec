# Constants

There are *boolean constants*, *rune constants*, *integer constants*, *floating-point constants*, *complex constants*, and *string constants*. Rune, integer, floating-point, and complex constants are collectively called *numeric constants*.

A constant value is represented by a [rune](/Lexical%20elements/rune_literals.html), [integer](/Lexical%20elements/integer_literals.html), [floating-point](/Lexical%20elements/floating-point_literals.html), [imaginary](/Lexical%20elements/imaginary_literals.html), or [string](/Lexical%20elements/string_literals.html) literal, an identifier denoting a constant, a [constant expression](/Expressions/constant_expressions.html), a [conversion](/Expressions/conversions.html) with a result that is a constant, or the result value of some built-in functions such as `unsafe.Sizeof` applied to any value, `cap` or `len` applied to [some expressions](/Built-in%20functions/length_and_capacity.html), ```real``` and `imag` applied to a complex constant and `complex` applied to numeric constants. The boolean truth values are represented by the predeclared constants `true` and `false`. The predeclared identifier [iota](/Declarations%20and%20scope/iota.html) denotes an integer constant.

In general, complex constants are a form of [constant expression](/Expressions/constant_expressions.html) and are discussed in that section.

Numeric constants represent exact values of arbitrary precision and do not overflow. Consequently, there are no constants denoting the IEEE-754 negative zero, infinity, and not-a-number values.

Constants may be [typed](/Types/) or *untyped*. Literal constants, `true`, `false`, `iota`, and certain [constant expressions](/Expressions/constant_expressions.html) containing only untyped constant operands are untyped.

A constant may be given a type explicitly by a [constant declaration](/Declarations%20and%20scope/constant_declarations.html) or [conversion](/Expressions/conversions.html), or implicitly when used in a [variable declaration](/Declarations%20and%20scope/variable_declarations.html) or an [assignment](/Statements/assignments.html) or as an operand in an [expression](/Expressions/). It is an error if the constant value cannot be represented as a value of the respective type. For instance, 3.0 can be given any integer or any floating-point type, while 2147483648.0 (equal to 1<<31) can be given the types `float32`, `float64`, or `uint32` but not `int32` or `string`.

An untyped constant has a *default type* which is the type to which the constant is implicitly converted in contexts where a typed value is required, for instance, in a [short variable declaration](/Declarations%20and%20scope/short_variable_declarations.html) such as i := 0 where there is no explicit type. The default type of an untyped constant is `bool`, `rune`, `int`, `float64`, `complex128` or `string` respectively, depending on whether it is a boolean, rune, integer, floating-point, complex, or string constant.

Implementation restriction: Although numeric constants have arbitrary precision in the language, a compiler may implement them using an internal representation with limited precision. That said, every implementation must:

Represent integer constants with at least 256 bits.
Represent floating-point constants, including the parts of a complex constant, with a mantissa of at least 256 bits and a signed binary exponent of at least 16 bits.
Give an error if unable to represent an integer constant precisely.
Give an error if unable to represent a floating-point or complex constant due to overflow.
Round to the nearest representable constant if unable to represent a floating-point or complex constant due to limits on precision.
These requirements apply both to literal constants and to the result of evaluating constant expressions.