# [상수 식(Constant expressions)](#constant-expressions)

* Go 버전: 1.9
* 원문: [Constant expressions](https://golang.org/ref/spec#Constant_expressions)
* 번역자: Sang-joon, Moon(@dakeshi)

Constant expressions may contain only [constant](/Constants/) operands and are evaluated at compile time.

상수 식(expression)은 컴파일 시 평가되며, [상수](/Constants/)로만 피연산자들을 구성할 수도 있다.

Untyped boolean, numeric, and string constants may be used as operands wherever it is legal to use an operand of boolean, numeric, or string type, respectively. Except for shift operations, if the operands of a binary operation are different kinds of untyped constants, the operation and, for non-boolean operations, the result use the kind that appears later in this list: integer, rune, floating-point, complex. For example, an untyped integer constant divided by an untyped complex constant yields an untyped complex constant.

불리언, 숫자, string 타입의 피연산자를 사용할 수 있는 곳이라면, 미지정 타입의 불리언, 숫자, 문자열 상수를 피연산자로 사용할 수도 있다. 시프트 연산을 제외하고 이항 연산자의 피연산자가 서로 다른 미지정 타입의 상수일 때, 연산(불리언 연산은 제외) 및 결과의 타입은 다음과 같은 순서로 결정된다: 복소수 상수가 가장 우선되며, 부동 소수점, 룬, 정수 상수 순이다. 예를 들어, 미지정 타입의 정수 상수를 미지정 타입의 복소수 상수로 나눈 결과는 미지정 타입의 복소수 상수다.

A constant [comparison](/Expressions/comparison_operators.html) always yields an untyped boolean constant. If the left operand of a constant [shift expression](/Expressions/operators.html) is an untyped constant, the result is an integer constant; otherwise it is a constant of the same type as the left operand, which must be of [integer type](/Types/numeric_types.html). Applying all other operators to untyped constants results in an untyped constant of the same kind (that is, a boolean, integer, floating-point, complex, or string constant).

상수들 간의 [비교](/Expressions/comparison_operators.html) 결과는 항상 미지정 타입의 불리언 상수다. 왼쪽 피연산자가 미지정 타입의 상수인 상수 [시프트 식](/Expressions/operators.html)의 결과는 정수 상수다; 왼쪽 피연산자가 미지정 타입의 상수가 아닌 경우도 결과는 [정수](/Types/numeric_types.html) 상수다. 이외의 연산자들을 미지정 타입의 상수와 함께 사용하면, 그 결과는 같은 종류의 미지정 상수다. (즉, 불리언, 정수, 부동 소수점, 복소수, 문자열 상수)

```
const a = 2 + 3.0          // a == 5.0   (untyped floating-point constant)
const b = 15 / 4           // b == 3     (untyped integer constant)
const c = 15 / 4.0         // c == 3.75  (untyped floating-point constant)
const Θ float64 = 3/2      // Θ == 1.0   (type float64, 3/2 is integer division)
const Π float64 = 3/2.     // Π == 1.5   (type float64, 3/2. is float division)
const d = 1 << 3.0         // d == 8     (untyped integer constant)
const e = 1.0 << 3         // e == 8     (untyped integer constant)
const f = int32(1) << 33   // illegal    (constant 8589934592 overflows int32)
const g = float64(2) >> 1  // illegal    (float64(2) is a typed floating-point constant)
const h = "foo" > "bar"    // h == true  (untyped boolean constant)
const j = true             // j == true  (untyped boolean constant)
const k = 'w' + 1          // k == 'x'   (untyped rune constant)
const l = "hi"             // l == "hi"  (untyped string constant)
const m = string(k)        // m == "x"   (type string)
const Σ = 1 - 0.707i       //            (untyped complex constant)
const Δ = Σ + 2.0e-4       //            (untyped complex constant)
const Φ = iota*1i - 1/1i   //            (untyped complex constant)
```

```
const a = 2 + 3.0          // a == 5.0   (미지정 타입의 부동 소수점 상수)
const b = 15 / 4           // b == 3     (미지정 타입의 정수 상수)
const c = 15 / 4.0         // c == 3.75  (미지정 타입의 부동 소수점 상수)
const Θ float64 = 3/2      // Θ == 1.0   (float64 타입, 3/2은 정수 나눗셈)
const Π float64 = 3/2.     // Π == 1.5   (float64 타입, 3/2.은 부동 소수점 나눗셈)
const d = 1 << 3.0         // d == 8     (미지정 타입의 정수 상수)
const e = 1.0 << 3         // e == 8     (미지정 타입의 정수 상수)
const f = int32(1) << 33   // 허용 안됨    (상수 8589934592는 int32 크기를 오버플로우하기 때문에 허용되지 않음)
const g = float64(2) >> 1  // 허용 안됨    (float64(2)는 부동 소수점 상수이기 때문에 허용되지 않음)
const h = "foo" > "bar"    // h == true  (미지정 타입의 불리언 상수)
const j = true             // j == true  (미지정 타입의 불리언 상수)
const k = 'w' + 1          // k == 'x'   (미지정 타입의 룬 상수)
const l = "hi"             // l == "hi"  (미지정 타입의 문자열 상수)
const m = string(k)        // m == "x"   (string 타입)
const Σ = 1 - 0.707i       //            (미지정 타입의 복소수 상수)
const Δ = Σ + 2.0e-4       //            (미지정 타입의 복소수 상수)
const Φ = iota*1i - 1/1i   //            (미지정 타입의 복소수 상수)
```

Applying the built-in function complex to untyped integer, rune, or floating-point constants yields an untyped complex constant.

미지정 타입의 정수 상수, 룬 상수, 부동 소수점 상수에 내장 함수 `complex`를 적용한 결과는 미지정 타입의 복소수 상수다.

```
const ic = complex(0, c)   // ic == 3.75i  (untyped complex constant)
const iΘ = complex(0, Θ)   // iΘ == 1i     (type complex128)
```

```
const ic = complex(0, c)   // ic == 3.75i  (미지정 타입의 복소수 상수)
const iΘ = complex(0, Θ)   // iΘ == 1i     (complex128 타입)
```

Constant expressions are always evaluated exactly; intermediate values and the constants themselves may require precision significantly larger than supported by any predeclared type in the language. The following are legal declarations:

상수 식은 항상 정확하게 평가된다(evaluated); 중간 단계의 값(intermediate value)과 상수 자체는 언어에서 미리 선언된 타입이 지원하는 것보다 훨씬 더 큰 정밀도가 요구된다. 아래의 선언문은 정상적으로 동작한다:

```
const Huge = 1 << 100         // Huge == 1267650600228229401496703205376  (미지정 타입의 정수 상수)
const Four int8 = Huge >> 98  // Four == 4                                (int8 타입)
```

The divisor of a constant division or remainder operation must not be zero:

상수의 나눗셈 연산 또는 나머지 연산에서 나누는 수는 0(zero)이 아니어야 한다.

```
3.14 / 0.0   // illegal: division by zero
```

```
3.14 / 0.0   // 허용 안됨: 0으로 나눴음
```

The values of typed constants must always be accurately representable as values of the constant type. The following constant expressions are illegal:

*타입* 정보가 있는 상수의 값은 상수 타입의 값으로 항상 정확하게 표현할 수 있어야 한다. 아래의 상수 식은 허용되지 않는다:

```
uint(-1)     // -1 cannot be represented as a uint
int(3.14)    // 3.14 cannot be represented as an int
int64(Huge)  // 1267650600228229401496703205376 cannot be represented as an int64
Four * 300   // operand 300 cannot be represented as an int8 (type of Four)
Four * 100   // product 400 cannot be represented as an int8 (type of Four)
```

```
uint(-1)     // unit 타입으로는 -1을 표현할 수 없다
int(3.14)    // int 타입으로는 3.14를 표현할 수 없다
int64(Huge)  // int64 타입으로는 1267650600228229401496703205376을 표현할 수 없다
Four * 300   // Four의 타입인 int8로는 피연산자 300을 표현할 수 없다.
Four * 100   // Four의 타입인 int8로는 곱셈의 결과인 400을 표현할 수 없다.
```

The mask used by the unary bitwise complement operator ^ matches the rule for non-constants: the mask is all 1s for unsigned constants and -1 for signed and untyped constants.

단항 비트 보수 연산자 `^`에서 사용하는 마스크(mask)는 산술(arithmetic) 연산 규칙을 따른다: 부호 없는 상수에 대해서는 마스크가 1이 적용되고, 부호 있는 미지정 타입의 상수에 대해서는 -1이 적용된다.

```
^1         // untyped integer constant, equal to -2
uint8(^1)  // illegal: same as uint8(-2), -2 cannot be represented as a uint8
^uint8(1)  // typed uint8 constant, same as 0xFF ^ uint8(1) = uint8(0xFE)
int8(^1)   // same as int8(-2)
^int8(1)   // same as -1 ^ int8(1) = -2
```

```
^1         // 미지정 타입의 정수 상수이며 -2와 같다
uint8(^1)  // 허용 안됨: uint8(-2)와 같고 uint8 타입으로는 -2를 표현할 수 없다
^uint8(1)  // uint8 타입의 상수이며 0xFF ^ uint8(1) = uint8(0xFE)와 같다
int8(^1)   // int8(-2)와 같다
^int8(1)   // -1 ^ int8(1) = -2와 같다
```

Implementation restriction: A compiler may use rounding while computing untyped floating-point or complex constant expressions; see the implementation restriction in the section on [constants](/Constants/). This rounding may cause a floating-point constant expression to be invalid in an integer context, even if it would be integral when calculated using infinite precision, and vice versa.

구현 제한: 컴파일러가 미지정 타입의 부동 소수점 또는 복소수 상수 식을 계산할 때 라운딩(rounding)을 사용하기도 한다; [상수](/Constants/) 섹션의 구현 제한을 참조하라. 무한 정밀도를 사용해 계산할 때 통합하더라도, 라운딩으로 인해 정수 타입을 처리하는 곳에서는 부동 소수점 상수 식이 제대로 동작하지 않을 수도 있다. 반대의 경우도 마찬가지다.