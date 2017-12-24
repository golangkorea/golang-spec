# [숫자 타입(Numeric types)](#numeric-types)

* Go 버전: 1.9
* 원문: [Numeric types](https://golang.org/ref/spec#Numeric_types)
* 번역자: JungSoo Ahn (@findstar)

A *numeric type* represents sets of integer or floating-point values. The predeclared architecture-independent numeric types are:

*숫자 타입*은 정수 또는 부동 소수점 값 세트를 나타낸다. 미리 선언된 숫자 타입 중 아키텍처 독립적인 숫자 타입은 다음과 같다:

```
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
```

```
uint8       부호 없는 모든  8비트 정수 (0 to 255)
uint16      부호 없는 모든 16비트 정수 (0 to 65535)
uint32      부호 없는 모든 32비트 정수 (0 to 4294967295)
uint64      부호 없는 모든 64비트 정수 (0 to 18446744073709551615)

int8        부호 있는 모든  8비트 정수 (-128 to 127)
int16       부호 있는 모든 16비트 정수 (-32768 to 32767)
int32       부호 있는 모든 32비트 정수 (-2147483648 to 2147483647)
int64       부호 있는 모든 64비트 정수 (-9223372036854775808 to 9223372036854775807)

float32     IEEE-754 32비트 모든 부동 소수점 숫자
float64     IEEE-754 64비트 모든 부동 소수점 숫자

complex64   float32의 실수와 허수로 구성된 모든 복소수
complex128  float64의 실수와 허수로 구성된 모든 복소수

byte        uint8의 별칭(alias)
rune        int32의 별칭(alias)
```

The value of an *n*-bit integer is *n* bits wide and represented using [two's complement arithmetic](http://en.wikipedia.org/wiki/Two's_complement).

*n*-비트의 정수 값은 *n*비트의 폭을 가지며 [2의 보수 산술](http://en.wikipedia.org/wiki/Two's_complement)을 사용하여 표시된다.

There is also a set of predeclared numeric types with implementation-specific sizes:

미리 선언된 숫자 타입 중 구현에 따라 그 크기가 달라지는 경우도 있다:

```
uint     either 32 or 64 bits
int      same size as uint
uintptr  an unsigned integer large enough to store the uninterpreted bits of a pointer value
```

```
uint     32비트 또는 64비트
int      uint와 동일한 사이즈
uintptr  포인터 값이면서 (아직 타입으로) 해석되지 않은 비트들를 저장할 만큼 크고, 부호가 없는 정수
```

To avoid portability issues all numeric types are distinct except `byte`, which is an alias for `uint8`, and `rune`, which is an alias for `int32`. Conversions are required when different numeric types are mixed in an expression or assignment. For instance, `int32` and `int` are not the same type even though they may have the same size on a particular architecture.

`unit8`의 별칭(alias)인 `byte`, `int32` 의 별칭(alias)인 `rune`을 제외한 모든 숫자 타입이 서로 다르기 때문에 이식성(portability) 문제를 피할 수 있다. 식(expression)이나 할당에 서로 다른 숫자 타입이 함께 사용된 경우, 변환(conversion)이 필요하다. 예를 들어, `int32` 와 `int`가 특정 아키텍처 환경에서 같은 크기일 수는 있지만 같은 타입은 아니다.
