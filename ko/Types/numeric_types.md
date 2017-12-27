# [숫자 타입](#numeric-types)

* Go 버전: 1.9
* 원문: [Numeric types](https://golang.org/ref/spec#Numeric_types)
* 번역자: JungSoo Ahn (@findstar)

*숫자 타입*은 정수 또는 부동 소수점 값 집합을 나타낸다. 미리 선언된 숫자 타입 중 아키텍처 독립적인 숫자 타입은 다음과 같다:

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

*n*-비트의 정수 값은 *n* 비트의 폭을 가지며 [2의 보수 산술](http://en.wikipedia.org/wiki/Two's_complement)을 사용하여 표시된다.

미리 선언된 숫자 타입 중 구현에 따라 그 크기가 달라지는 경우도 있다:

```
uint     32비트 또는 64비트
int      uint와 동일한 사이즈
uintptr  포인터 값이면서 (아직 타입으로) 해석되지 않은 비트들를 저장할 만큼 크고, 부호가 없는 정수
```

`unit8`의 별칭(alias)인 `byte`, `int32` 의 별칭(alias)인 `rune`을 제외한 모든 숫자 타입이 서로 다르기 때문에 이식성(portability) 문제를 피할 수 있다. 식(expression)이나 할당에 서로 다른 숫자 타입이 함께 사용된 경우, 변환(conversion)이 필요하다. 예를 들어, `int32` 와 `int`가 특정 아키텍처 환경에서 같은 크기일 수는 있지만 같은 타입은 아니다.
