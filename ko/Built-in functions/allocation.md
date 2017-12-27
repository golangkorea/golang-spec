# [할당](#allocation)

* Go 버전: 1.9
* 원문: [Allocation](https://golang.org/ref/spec#Allocation)
* 번역자: Joseph Kim (@superbmilkyway)

내장 함수 `new`는 타입 `T`를 받고, 런타임 시점에 해당 타입 [변수](/Variables/)를 위한 저장 공간을 할당하고 해당 공간을 [가리키는](/Types/pointer_types.html) `*T` 타입의 값을 반환한다. 해당 변수는 초기화되며 변수 초기화와 관련해서는 [초기값](/Program initialization and execution/the_zero_value.html)절을 참조하라.

```golng
new(T)
```

예를 들어, 다음 코드는

```golang
type S struct { a int; b float64 }
new(S)
```

`S` 타입의 변수를 위한 저장 공간을 할당하고, 해당 변수를(`a=0`, `b=0.0`)으로 초기화 하고 해당 공간의 주소를 담고 있는 `*S` 타입의 값을 반환한다.
