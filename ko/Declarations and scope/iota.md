# [Iota](#iota)

[상수 선언문](/Declarations%20and%20scope/constant_declarations.html) 안에서 미리 선언된 식별자인 `iota`는 연속된 미지정 타입의 정수 [상수](/Constants/)를 나타낸다. 소스코드에서 예약어인 `const`를 사용할 때마다 iota는 0으로 리셋되고 [ConstSpec](/Declarations%20and%20scope/constant_declarations.html#ConstSpec)가 나타날 때마다 값이 증가한다. 서로 관련있는 상수 집합을 구성할 때 iota를 사용할 수 있다.

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
    u         = iota * 42  // u == 0     (미지정 타입 정수 상수)
    v float64 = iota * 42  // v == 42.0  (float64 상수)
    w         = iota * 42  // w == 84    (미지정 타입 정수 상수)
)

const x = iota  // x == 0  (iota는 리셋됨.)
const y = iota  // y == 0  (iota는 리셋됨.)
```

ConstSpec 가 나타난 이후에만 증가하기 때문에 ExpressionList 내에서는 각 `iota`값이 모두 같다.

```go
const (
    bit0, mask0 = 1 << iota, 1<<iota - 1  // bit0 == 1, mask0 == 0
    bit1, mask1                           // bit1 == 2, mask1 == 1
    _, _                                  // iota == 2 는 건너뜀
    bit3, mask3                           // bit3 == 8, mask3 == 7
)
```

마지막 예제코드는 마지막으로 사용된 비어있지 않은 식 목록을 암묵적으로 반복해서 사용한다

