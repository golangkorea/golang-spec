# [슬라이스, map과 채널 생성](#making_slices,_maps_and_channels)

내장 함수 `make`는 `T` 타입을 인자로 사용하며 가능한 타입은 슬라이스, map, 채널 타입이다.  또한, 해당 타입과 관련된 식(expression)이 인자에 추가될 수 있다. 이 함수는 `T` 타입(`*T`가 아님)의 값을 반환한다. 이 메모리는 [초기 값](/Program%20initialization%20and%20execution/the_zero_value.html) 섹션에서 설명하는 바와 같이 초기화 된다.

```go
호출             타입 T     결과

make(T, n)       슬라이스      길이 n과 용량 n을 갖는 T 타입의 슬라이스
make(T, n, m)    슬라이스      길이 n과 용량 m을 갖는 T 타입의 슬라이스

make(T)          map        T 타입의 map
make(T, n)       map        약 n개의 요소를 위한 초기 공간을 갖는 T 타입의 map

make(T)          채널    버퍼되지 않는 T 타입의 채널
make(T, n)       채널    n만큼의 버퍼 크기를 갖는 버퍼되는 T 타입의 채널
```

크기 인자인 `n`과 `m`은 정수 타입이거나 미지정 타입이어야 한다. [상수](/Constants/) 크기 인자는 음수가 아니어야 하고, `int` 타입의 값으로 표현될 수 있어야 한다. `n`과 `m`이 모두 상수로 제공된다면, `n`은 `m`보다 커서는 안된다. 실행 시간 동안에 `n`이 음수이거나 `m`보다 크다면, [런타임 패닉](/Run-time%20panics/)이 발생한다.

```go
s := make([]int, 10, 100)       // len(s) == 10, cap(s) == 100의 슬라이스
s := make([]int, 1e3)           // len(s) == cap(s) == 1000의 슬라이스
s := make([]int, 1<<63)         // 허용안됨: len(s)이 int 타입의 값으로 표현될 수 없음
s := make([]int, 10, 0)         // 허용안됨: len(s) > cap(s)
c := make(chan int, 10)         // 버퍼 크기 10을 갖는 채널
m := make(map[string]int, 100)  // 약 100여개의 요소에 대한 초기 공간이 있는 map
```

map 타입과 크기 정보 `n`을 취하는 `make` 호출은 `n`개의 map 요소에 대한 초기 공간을 갖는 map을 만든다. 이러한 생성의 정확한 동작은 구현에 의존한다.
