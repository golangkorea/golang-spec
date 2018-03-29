# [Iota](#iota)

미리 선언된 식별자인, `iota`가 [상수 선언](/Declarations%20and%20scope/constant_declarations.html)내 사용되면 미지정 타입의 연속된 정수 [상수](/Constants/)를 나타낸다. 예약어인, `const`가 소스코드에 나타날 때마다 0으로 리셋되고 매번 [ConstSpec](/Declarations%20and%20scope/constant_declarations.html#ConstSpec) 이후에 값이 증가한다. 서로 관련있는 상수들 집합을 구성하는데 사용될 수 있다:

```go
const ( // iota는 0으로 리셋된다.
    c0 = iota  // c0 == 0
    c1 = iota  // c1 == 1
    c2 = iota  // c2 == 2
)

const ( // iota는 0으로 리셋된다.
    a = 1 << iota  // a == 1
    b = 1 << iota  // b == 2
    c = 3          // c == 3  (iota가 사용되지 않았지만 계속 증가한다)
    d = 1 << iota  // d == 8
)

const ( // iota는 0으로 리셋된다.
    u         = iota * 42  // u == 0     (미지정 정수 상수)
    v float64 = iota * 42  // v == 42.0  (float64 상수)
    w         = iota * 42  // w == 84    (미지정 정수 상수)
)

const x = iota  // x == 0  (iota는 리셋되었다.)
const y = iota  // y == 0  (iota는 리셋되었다.)
```

ConstSpec 이후에만 증가하기 때문에 ExpressionList내에서는 각 `iota`값이 모두 같다.

```go
const (
    bit0, mask0 = 1 << iota, 1<<iota - 1  // bit0 == 1, mask0 == 0
    bit1, mask1                           // bit1 == 2, mask1 == 1
    _, _                                  // iota == 2 는 건너뜀
    bit3, mask3                           // bit3 == 8, mask3 == 7
)
```

이 마지막 예제는 마지막으로 사용된 표현식의 목록을 암시적으로 반복하여 사용합니다.

