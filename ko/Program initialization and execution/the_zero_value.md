# [제로값](#the-zero-value)

선언문이나 `new`를 통해서 하나의 [변수](/Variables/)에 저장공간이 할당될 때, 합성 문자값(composite literal)이나 `make`를 통해 새로운 값이 만들어 질때, 초기화가 명시되지 않았다면, 이러한 변수와 새로운 값에 기정값(default value)가 주어진다. 그러한 변수나 값의 개별 요소에는 타입에 맞추어 다음과 같은 *제로값*이 설정된다: boolean들은 `false`, integer들은 0, float들은 0.0, string에는 ""가 설정되며 포인터, 함수, 인터페이스, 슬라이스, 채널, 그리고 맵에는 `nil`이 설정된다. 이러한 초기화는 재귀적으로 적용되는데, 예를 들어 구조체의 정렬(array)의 각 요소들 내부의 모든 필드들은 값이 명시되지 않았을 경우 제로값을 가지게 될 것이다.

다음의 간단한 두 선언문은 동일하다.

```go
var i int
var i int = 0
```

아래의 코드가 실행되면

```go
type T struct { i int; f float64; next *T }
t := new(T)
```

다음과 같은 결과가 나타난다.

```go
t.i == 0
t.f == 0.0
t.next == nil
```

아래와 같이 실행해도 같은 결과가 나온다.

```go
var t T
```