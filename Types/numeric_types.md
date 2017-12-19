# [숫자 타입(Numeric types)](#numeric-types)

* Go 버전: 1.9
* 원문: [Numeric types](https://golang.org/ref/spec#Numeric_types)
* 번역자: JungSoo Ahn (@findstar)

A *numeric type* represents sets of integer or floating-point values. The predeclared architecture-independent numeric types are:

*numeric 타입*은 정수 또는 부동 소수점 값 세트를 나타낸다. 아키텍처에 관계없이 미리 선언된 숫자 타입은 다음과 같:

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
uint8       모든 부호 없는  8비트 정수 (0 to 255)
uint16      모든 부호 없는 16비트 정수 (0 to 65535)
uint32      모든 부호 없는 32비트 정수 (0 to 4294967295)
uint64      모든 부호 없는 64비트 정수 (0 to 18446744073709551615)

int8        모든 부호가 존재하는  8비트 정수 (-128 to 127)
int16       모든 부호가 존재하는 16비트 정수 (-32768 to 32767)
int32       모든 부호가 존재하는 32비트 정수 (-2147483648 to 2147483647)
int64       모든 부호가 존재하는 64비트 정수 (-9223372036854775808 to 9223372036854775807)

float32     모든 IEEE-754 32비트 부동 소수점 숫자
float64     모든 IEEE-754 64비트 부동 소수점 숫자

complex64   float32의 모든 실수 및 허수의 복소수
complex128  float64의 모든 실수 및 허수의 복소수

byte        uint8의 별칭(alias)
rune        int32의 별칭(alias)
```

The value of an *n*-bit integer is *n* bits wide and represented using [two's complement arithmetic](http://en.wikipedia.org/wiki/Two's_complement).

*n*비트의 정수 값은 *n*비트의 폭을 가지며 [2의 보수 연산](http://en.wikipedia.org/wiki/Two's_complement)을 사용하여 표시된다.

There is also a set of predeclared numeric types with implementation-specific sizes:

구현시 최적화된 사이즈를 가지는 미리 선언된 숫자 타입도 있다:

```
uint     either 32 or 64 bits
int      same size as uint
uintptr  an unsigned integer large enough to store the uninterpreted bits of a pointer value
```

```
uint     32비트 또는 64비트
int      uint와 동일한 사이즈
uintptr  포인트 값의 해석되지 않은 비트를 저장하는데 충분히 큰 부호가 없는 정수
```

To avoid portability issues all numeric types are distinct except `byte`, which is an alias for `uint8`, and `rune`, which is an alias for `int32`. Conversions are required when different numeric types are mixed in an expression or assignment. For instance, `int32` and `int` are not the same type even though they may have the same size on a particular architecture.

이식성 문제를 회피하기 위해서 `unit8`의 별칭(alias)인 `byte`, `int32` 의 별칭(alias)인 `rune`을 제외한 모든 숫자 타입은 구분된다. 표현식(expression)이나 할당에서 다른 숫자 타입이 섞여 있다면, 변환을 필요로 한다. 예를 들어, `int32` 와 `int`는 특정 아키텍처에서 동일한 사이즈를 가질 수 있지만 동일한 타입이 아니다.
