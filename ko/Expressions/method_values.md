# [메서드 값](#method-values)

식 `x`가 정적 타입 `T`를 가지고 있고 `M`이 타입 `T`의 [메서드 집합](/Types/method_sets.html)에 속할 때, `x.M`를 *메서드 값*이라고 부른다. 메서드 값 `x.M`는 메서드로 `x.M`을 호출할 때 사용한 인자를 똑같이 사용해 호출할 수 있는 함수 값이다. 식 `x`는 메서드 값의 평가가 진행되는 동안 평가되고 저장된다; 저장된 복사본은 이후에 실행되는 모든 호출에 수신자로 사용된다. 

타입 `T`는 interface 타입일 수도 있고 아닐 수도 있다.

[메서드 식](/Expressions/method_expressions.html)에서도 예제로 사용했던 2개의 메서드를 가진 struct 타입 `T` 를 살펴보자. `Mv`는 `T` 타입의 수신자를,  `Mp`는 `*T` 타입의 수신자를 가지고 있다.

```go
type T struct {
    a int
}
func (tv  T) Mv(a int) int         { return 0 }  // 값 수신자
func (tp *T) Mp(f float32) float32 { return 1 }  // 포인터 수신자

var t T
var pt *T
func makeT() T
```

아래 식의 결과는

```go
t.Mv
```

아래와 같은 타입의 함수 값이다.

```go
func(int) int
```

아래의 두 가지 호출은 같은 것이다:

```go
t.Mv(7)
f := t.Mv; f(7)
```

유사하게, 아래 식의 결과는

```go
pt.Mp
```

아래와 같은 타입의 함수 값이다.

```go
func(float32) float32
```

[선택자](/Expressions/selectors.html) 챕터에서도 언급되었듯이, 값 수신자를 가진 interface 가 아닌 메서드를 포인터를 이용해 참조하면 자동적으로 해당 포인터를 역참조(dereference)한다: 즉 `pt.Mv`와 `(*pt).Mv`는 같다.

[메서드 호출](/Expressions/calls.html) 챕터에서 설명했듯이, 주소를 취할 수 있는 값을 사용해 포인터 수신자를 가진 interface가 아닌 메서드를 참조하면, 자동적으로 그 값의 주소를 취하게 된다: 즉, `t.Mp`와 `(&t).Mp`는 같다.

```go
f := t.Mv; f(7)   // t.Mv(7)과 같다
f := pt.Mp; f(7)  // pt.Mp(7)과 같다
f := pt.Mv; f(7)  // (*pt).Mv(7)과 같다
f := t.Mp; f(7)   // (&t).Mp(7)과 같다
f := makeT().Mp   // 허용되지 않음: makeT()의 결괏값에 대한 주소를 취할 수 없다
```

위의 예제에서는 interface 타입이 아닌 타입만 사용했지만, interface 타입의 값으로부터 메서드 값을 만드는 것도 허용된다.

```go
var i interface { M(int) } = myVal
f := i.M; f(7)  // i.M(7)과 같다
```
