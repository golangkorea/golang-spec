# [복소수 다루기](#manipulating_complex_numbers)

복소수의 결합 및 분해와 관련해 세 가지 함수가 제공된다. 내장 함수 `complex`는 부동 소수점 실수 부분과 허수 부분을 인자로 받아 복소수 값을 구성하며, `real`과 `imag` 함수는 각각 복소수 값에서 실수 부분, 허수 부분를 추출한다.

```go
complex(realPart, imaginaryPart floatT) complexT
real(complexT) floatT
imag(complexT) floatT
```

인자들의 타입과 반환 값은 대응된다. `complex`의 두 인자는 부동 소수점 타입이어야 하며, 반환 타입은 이에 대응되는 부동 소수점으로 구성되는 복소수 타입이다: `float32` 타입 인자들에 대해서는 `complex64`, `float64`  타입 인자들에 대해서는 `complex128`가 매칭된다. 인자들 중 하나가 미지정 타입의 상수로 평가되면, 먼저 다른 인자의 타입으로 [변환](/Expressions/conversions)된다. 두 개의 인자가 모두 미지정 타입의 상수로 평가된다면, 두 인자가 모두 복소수가 아니거나 허수 부분이 0이면서 함수의 반환 값이 미지정 타입의 복소수 상수여야만 한다.

`real`과 `imag`의 경우, 인자는 반드시 복소수 타입이어야 하며, 반환 타입은 이에 대응하는 부동 소수점 타입어어야만 한다: `complex64` 타입의 인자에 대해 `float32`, `complex128` 타입의 인자에 대해 `float64` 타입이 매칭된다. 인자가 미지정 타입의 상수로 평가된다면, 해당 인자는 숫자여야 하고, 함수의 반환 값은 미지정 타입의 부동 소수점 상수여야만 한다.

`real`과 `imag` 함수를 함께 사용하면 `complex` 함수의 정반대 역할을 수행하게 만들 수 있으며, 이로 인해 복소수 타입 `Z`의 `z` 값에 대해 `z == Z(complex(real(z), imag(z)))`가 성립한다.

이 함수들의 피연산자가 모두 상수라면 반환 값 또한 상수이다.

```go
var a = complex(2, -2)             // complex128
const b = complex(1.0, -1.4)       // 미지정 타입의 복소수 상수 1 - 1.4i
x := float32(math.Cos(math.Pi/2))  // float32
var c64 = complex(5, -x)           // complex64
var s uint = complex(1, 0)         // uint 타입으로 변환될 수 있는 미지정 타입의 복소수 상수 1 + 0i
_ = complex(1, 2<<s)               // 허용안됨: 2는 부동 소수점 타입으로 취급되며, 시프트 연산을 할 수 없음
var rl = real(c64)                 // float32
var im = imag(a)                   // float64
const c = imag(b)                  // 미지정 타입의 상수 -1.4
_ = imag(3 << s)                   // 허용안됨: 3은 복소수 타입으로 취급됨, 시프트 연산을 할 수 없음
```
