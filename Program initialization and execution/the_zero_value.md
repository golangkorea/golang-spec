# [제로값(The zero value)](#the-zero-value)

* Go 버전: 1.9
* 원문: [The zero value](https://golang.org/ref/spec#The_zero_value)
* 번역자: Jhonghee Park (@jhonghee)

When storage is allocated for a [variable](/Variables/), either through a declaration or a call of `new`, or when a new value is created, either through a composite literal or a call of `make`, and no explicit initialization is provided, the variable or value is given a default value. Each element of such a variable or value is set to the *zero value* for its type: `false` for booleans, 0 for integers, 0.0 for floats, "" for strings, and `nil` for pointers, functions, interfaces, slices, channels, and maps. This initialization is done recursively, so for instance each element of an array of structs will have its fields zeroed if no value is specified.

선언문이나 `new`를 통해서 하나의 [변수](/Variables/)에 저장공간이 할당될 때, 합성 문자값(composite literal)이나 `make`를 통해 새로운 값이 만들어 질때, 초기화가 명시되지 않았다면, 이러한 변수와 새로운 값에 기정값(default value)가 주어진다. 그러한 변수나 값의 개별 요소에는 타입에 맞추어 다음과 같은 *제로값*이 설정된다: boolean들은 `false`, integer들은 0, float들은 0.0, string에는 ""가 설정되며 포인터, 함수, 인터페이스, 슬라이스, 채널, 그리고 맵에는 `nil`이 설정된다. 이러한 초기화는 재귀적으로 적용되는데, 예를 들어 구조체의 정렬(array)의 각 요소들 내부의 모든 필드들은 값이 명시되지 않았을 경우 제로값을 가지게 될 것이다.

These two simple declarations are equivalent:

다음의 간단한 두 선언문은 동일하다.

```
var i int
var i int = 0
```

After

아래의 코드가 실행되면

```
type T struct { i int; f float64; next *T }
t := new(T)
```

the following holds:

다음과 같은 결과가 나타난다.

```
t.i == 0
t.f == 0.0
t.next == nil
```

The same would also be true after

아래와 같이 실행해도 같은 결과가 나온다.

```
var t T
```