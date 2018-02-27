# [할당](#allocation)

내장 함수 `new`은 `T` 타입을 인자로 사용하고, 런타임 시점에 해당 타입의 [변수](/Variables/)를 위한 저장 공간을 할당하며, 이 공간을 [가리키는](/Types/pointer_types.html) `*T` 타입의 값을 반환한다. 이 변수는 [초기값](/Program%20initialization%20and%20execution/the_zero_value.html)섹션에 설명하는 바와 같이 초기화된다. 

```go
new(T)
```

예를 들어, 다음 코드는

```go
type S struct { a int; b float64 }
new(S)
```

`S` 타입의 변수를 위한 저장 공간을 할당하고, 이 변수를(`a=0`, `b=0.0`)으로 초기화하며 저장 공간 주소를 담고 있는 `*S` 타입의 값을 반환한다.
