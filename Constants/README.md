# [상수 (Constants)](#constants)

* Go 버전: 1.9
* 원문: [Constants](https://golang.org/ref/spec#Constants)
* 번역자: Dong-Woo, Jeon(@a2600riz)

There are *boolean constants*, *rune constants*, *integer constants*, *floating-point constants*, *complex constants*, and *string constants*. Rune, integer, floating-point, and complex constants are collectively called *numeric constants*.

상수 타입으로는 *boolean 상수*, *룬 문자 상수*, *정수형 상수*, *부동소수점 상수*, *복소수 상수*, *문자열 상수*들이 있다. 룬 문자, 정수, 부동소수점, 복소수 상수들을 통칭해서 *수치 상수*라 칭한다.

A constant value is represented by a [rune](/Lexical%20elements/rune_literals.html), [integer](/Lexical%20elements/integer_literals.html), [floating-point](/Lexical%20elements/floating-point_literals.html), [imaginary](/Lexical%20elements/imaginary_literals.html), or [string literal](/Lexical%20elements/string_literals.html), an identifier denoting a constant, a [constant expression](/Expressions/constant_expressions.html), a [conversion](/Expressions/conversions.html) with a result that is a constant, or the result value of some built-in functions such as `unsafe.Sizeof` applied to any value, `cap` or `len` applied to [some expressions](/Built-in%20functions/length_and_capacity.html), `real` and `imag` applied to a complex constant and `complex` applied to numeric constants. The boolean truth values are represented by the predeclared constants `true` and `false`. The predeclared identifier [iota](/Declarations%20and%20scope/iota.html) denotes an integer constant.

상수 값은 [룬 문자](/Lexical%20elements/rune_literals.html), [정수](/Lexical%20elements/integer_literals.html), [부동소수점]((/Lexical%20elements/floating-point_literals.html)), [허수](/Lexical%20elements/imaginary_literals.html), [문자열 리터럴](/Lexical%20elements/string_literals.html), 상수 식별자, [상수 식](/Expressions/constant_expressions.html), [변환된 상수](/Expressions/conversions.html) 결과값 또는 `unsafe.Sizeof` 같은 몇몇 내장 함수들의 결과값이 적용된 값, `cap` 또는 `len`이 적용된 [몇 가지 식](/Built-in%20functions/length_and_capacity.html), `real`와 `imag`가 적용된 복소수 상수와 `complex`가 적용된 수치 상수로 표현된다. boolean 값은 미리 선언되어 있는 `true` 와 `false` 값으로 표현된다. 미리 선언된 식별자 [iota](/Declarations%20and%20scope/iota.html)는 정수형 상수값을 의미한다.

In general, complex constants are a form of [constant expression](/Expressions/constant_expressions.html) and are discussed in that section.

일반적으로 복소수 상수들은 [상수 식](/Expressions/constant_expressions.html)이며 이는 현재 섹션에서 설명될 것이다.

Numeric constants represent exact values of arbitrary precision and do not overflow. Consequently, there are no constants denoting the IEEE-754 negative zero, infinity, and not-a-number values.

수치 상수들은 임의적 정밀도(arbitrary precision)의 정확한 값으로 표현되며 오버플로우(overflow) 되지 않는다. 따라서 IEEE-754 negative zero, 무한, 숫자값이 아닌 값으로 표시되는 상수들은 없다.

Constants may be [typed](/Types/) or *untyped*. Literal constants, `true`, `false`, `iota`, and certain [constant expressions](/Expressions/constant_expressions.html) containing only untyped constant operands are untyped.

상수는 [지정된 타입(typed)](/Types/)이거나 *비지정된 타입(untyped)*일수 있다. 상수 리터럴, `true`, `false`, `iota` 들과 오직 비지정 타입 피연산자 상수들만 포함하는 특정 [상수 식](/Expressions/constant_expressions.html)들은 비지정 타입이다.

A constant may be given a type explicitly by a [constant declaration](/Declarations%20and%20scope/constant_declarations.html) or [conversion](/Expressions/conversions.html), or implicitly when used in a [variable declaration](/Declarations%20and%20scope/variable_declarations.html) or an [assignment](/Statements/assignments.html) or as an operand in an [expression](/Expressions/). It is an error if the constant value cannot be represented as a value of the respective type. For instance, 3.0 can be given any integer or any floating-point type, while 2147483648.0 (equal to 1<<31) can be given the types `float32`, `float64`, or `uint32` but not `int32` or `string`.

어떤 [상수의 선언](/Declarations%20and%20scope/constant_declarations.html) 또는 [변환](/Expressions/conversions.html)에 의해서, 또는 암시적으로 어떤 변수에 [할당](/Statements/assignments.html) 또는 [선언](/Declarations%20and%20scope/variable_declarations.html) 할때, 아니면 어떤 [식](/Expressions/)의 피연산자로서 사용될때 타입은 명시적으로 주어질수 있다. 만약 상수값이 각각의 타입의 값으로 표현되지 못한다면 에러가 발생한다. 예를 들어, 3.0은 어떤 정수형 또는 아무 부동 소수점 타입으로 지정될 수 있으며, 2147483648.0( 1 << 31와 동일 )에는 `float32`, `float64` 또는 `uint32`와 같은 타입이 주어질 수 있지만 `int32` 또는 `string`은 2147483648.0의 타입이 되지 못한다.

An untyped constant has a *default type* which is the type to which the constant is implicitly converted in contexts where a typed value is required, for instance, in a [short variable declaration](/Declarations%20and%20scope/short_variable_declarations.html) such as i := 0 where there is no explicit type. The default type of an untyped constant is `bool`, `rune`, `int`, `float64`, `complex128` or `string` respectively, depending on whether it is a boolean, rune, integer, floating-point, complex, or string constant.

비지정 타입 상수는 타입 지정된 값이 필요한 문맥, 예를 들어 명시적 타입이 없는 i := 0 같은 [짧은 변수 선언](/Declarations%20and%20scope/short_variable_declarations.html)에서 암시적으로 변환된 타입이 *기본 타입*으로 지정된다. 비지정 타입 상수의 기본 타입은 비지정 타입 상수가 boolean, 룬 문자, 정수, 부동소수점, 복소수, 또는 문자열 상수이냐 아니냐에 따라 각각 `bool`, `rune`, `int`, `float64`, `complex128` 또는 `string` 이 된다.

Implementation restriction: Although numeric constants have arbitrary precision in the language, a compiler may implement them using an internal representation with limited precision. That said, every implementation must:

* Represent integer constants with at least 256 bits.
* Represent floating-point constants, including the parts of a complex constant, with a mantissa of at least 256 bits and a signed exponent of at least 32 bits.
* Give an error if unable to represent an integer constant precisely.
* Give an error if unable to represent a floating-point or complex constant due to overflow.
* Round to the nearest representable constant if unable to represent a floating-point or complex constant due to limits on precision.

구현 제한: 수치 상수가 언어상에서 임의적 정밀도를 가짐에도 불구하고, 컴파일러는 제한된 정확도로 내부적인 표현방식을 써서 그것들을 구현할 것이다. 이 말은 즉, 모든 구현은 반드시:

* 최소 256 비트의 정수 상수로 표현되야 한다.
* 최소 256 비트의 가수와 최소 16비트의 부호가 있는 이진 지수와 함께 복소수 상수의 부분을 포함하여 부동소수점 상수를 표현해야 한다.
* 정확하게 표현할 수 없는 정수형 상수가 있다면 에러를 발생시켜야 한다.
* 오버플로우 때문에 정확하게 표현할 수 없는 부동소수점 또는 복소수 상수가 있다면 에러를 발생시켜야 한다.
* 정밀도 제한 때문에 부동소수점 또는 복소수 상수를 표현하지 못한다면 가장 가깝게 표현 가능한 상수로 반올림 해야 한다.

These requirements apply both to literal constants and to the result of evaluating constant expressions.

이 요구사항들은 리터럴 상수와 상수 식의 평가 결과 모두에게 적용된다.
