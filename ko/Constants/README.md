# [상수](#constants)

상수 타입으로는 *boolean 상수*, *룬 문자 상수*, *정수형 상수*, *부동소수점 상수*, *복소수 상수*, *문자열 상수*들이 있다. 룬 문자, 정수, 부동소수점, 복소수 상수들을 통칭해서 *수치 상수*라 칭한다.

상수 값은 [룬 문자](/Lexical%20elements/rune_literals.html), [정수](/Lexical%20elements/integer_literals.html), [부동소수점]((/Lexical%20elements/floating-point_literals.html)), [허수](/Lexical%20elements/imaginary_literals.html), [문자열 리터럴](/Lexical%20elements/string_literals.html), 상수 식별자, [상수 식](/Expressions/constant_expressions.html), [변환된 상수](/Expressions/conversions.html) 결과값 또는 `unsafe.Sizeof` 같은 몇몇 내장 함수들의 결과값이 적용된 값, `cap` 또는 `len`이 적용된 [몇 가지 식](/Built-in%20functions/length_and_capacity.html), `real`와 `imag`가 적용된 복소수 상수와 `complex`가 적용된 수치 상수로 표현된다. boolean 값은 미리 선언되어 있는 `true` 와 `false` 값으로 표현된다. 미리 선언된 식별자 [iota](/Declarations%20and%20scope/iota.html)는 정수형 상수값을 의미한다.

일반적으로 복소수 상수들은 [상수 식](/Expressions/constant_expressions.html)이며 이는 현재 섹션에서 설명될 것이다.

수치 상수들은 임의적 정밀도(arbitrary precision)의 정확한 값으로 표현되며 오버플로우(overflow) 되지 않는다. 따라서 IEEE-754 negative zero, 무한, 숫자값이 아닌 값으로 표시되는 상수들은 없다.

상수는 [지정된 타입(typed)](/Types/)이거나 *비지정된 타입(untyped)*일수 있다. 상수 리터럴, `true`, `false`, `iota` 들과 오직 비지정 타입 피연산자 상수들만 포함하는 특정 [상수 식](/Expressions/constant_expressions.html)들은 비지정 타입이다.

어떤 [상수의 선언](/Declarations%20and%20scope/constant_declarations.html) 또는 [변환](/Expressions/conversions.html)에 의해서, 또는 암시적으로 어떤 변수에 [할당](/Statements/assignments.html) 또는 [선언](/Declarations%20and%20scope/variable_declarations.html) 할때, 아니면 어떤 [식](/Expressions/)의 피연산자로서 사용될때 타입은 명시적으로 주어질수 있다. 만약 상수값이 각각의 타입의 값으로 표현되지 못한다면 에러가 발생한다. 예를 들어, 3.0은 어떤 정수형 또는 아무 부동 소수점 타입으로 지정될 수 있으며, 2147483648.0( 1 << 31와 동일 )에는 `float32`, `float64` 또는 `uint32`와 같은 타입이 주어질 수 있지만 `int32` 또는 `string`은 2147483648.0의 타입이 되지 못한다.

비지정 타입 상수는 타입 지정된 값이 필요한 문맥, 예를 들어 명시적 타입이 없는 i := 0 같은 [짧은 변수 선언](/Declarations%20and%20scope/short_variable_declarations.html)에서 암시적으로 변환된 타입이 *기본 타입*으로 지정된다. 비지정 타입 상수의 기본 타입은 비지정 타입 상수가 boolean, 룬 문자, 정수, 부동소수점, 복소수, 또는 문자열 상수이냐 아니냐에 따라 각각 `bool`, `rune`, `int`, `float64`, `complex128` 또는 `string` 이 된다.

구현 제한: 수치 상수가 언어상에서 임의적 정밀도를 가짐에도 불구하고, 컴파일러는 제한된 정확도로 내부적인 표현방식을 써서 그것들을 구현할 것이다. 이 말은 즉, 모든 구현은 반드시:

* 최소 256 비트의 정수 상수로 표현되야 한다.
* 최소 256 비트의 가수와 최소 16비트의 부호가 있는 이진 지수와 함께 복소수 상수의 부분을 포함하여 부동소수점 상수를 표현해야 한다.
* 정확하게 표현할 수 없는 정수형 상수가 있다면 에러를 발생시켜야 한다.
* 오버플로우 때문에 정확하게 표현할 수 없는 부동소수점 또는 복소수 상수가 있다면 에러를 발생시켜야 한다.
* 정밀도 제한 때문에 부동소수점 또는 복소수 상수를 표현하지 못한다면 가장 가깝게 표현 가능한 상수로 반올림 해야 한다.

이 요구사항들은 리터럴 상수와 상수 식의 평가 결과 모두에게 적용된다.
