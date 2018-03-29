# [메서드 값](#method-values)

식 `x`가 정적 타입 `T`를 가지고 있고 `M`이 타입 `T`의 [메서드 집합](/Types/method_sets.html)에 속하면, `x.M`는 *메서드 값*이라고 불린다. 메서드 값 `x.M`는 함수 값으로 `x.M`의 메서드 호출과 같은 인자를 가지고 호출된다. 식 `x`는 메서드 값의 평가가 진행되는 동안 평가되고 저장된다; 그런 다음 저장된 복사본은 리시버로서 이후에 실행될 수도 있는 어떤 호출에든 사용된다.

타입 `T`는 인터페이스 타입일 수도 있고 아닐 수도 있다.

[메서드 식](/Expressions/method_expressions.html)에서 토론한 바와 같이, 2개의 메서드를 가지는 struct 타입 `T`을 검토해 보자. `Mv`는 리시버 타입이 `T`인 메서드이고, `Mp`는 리시버 타입이 `*T`인 메서드이다.

```go
type T struct {
    a int
}
func (tv  T) Mv(a int) int         { return 0 }  // 리시버가 값인 경우
func (tp *T) Mp(f float32) float32 { return 1 }  // 리시버가 포인터인 경우

var t T
var pt *T
func makeT() T
```

아래 식은

```go
t.Mv
```

아래와 같은 타입의 함수 값을 생산한다.

```go
func(int) int
```

다음의 두 실행방식은 동등한다:

```go
t.Mv(7)
f := t.Mv; f(7)
```

유사하게, 아래의 식은

```go
pt.Mp
```

아래와 같은 타입의 함수 값을 생산한다.

```go
func(float32) float32
```

[선택자](/Expressions/selectors.html)에서 살펴 본 것처럼, 포인터를 사용하여 값-리시버로 인터페이스가 아닌 메서드를 참조하게 되면 자동적으로 그 포인터를 디레퍼런스한다: `pt.Mv`는 `(*pt).Mv`와 동등하다.

[메서드 호출](/Expressions/calls.html)에서 살펴본 바와 같이, 주소를 취할 수 있는 값을 사용하여 포인터 리시버로 인터페이스가 아닌 메서드를 참조하게 되면 자동적으로 그 값의 주소를 취하게 된다: `t.Mp`는 `(&t).Mp`와 동등한다.

```go
f := t.Mv; f(7)   // t.Mv(7)와 같다
f := pt.Mp; f(7)  // pt.Mp(7)와 같다
f := pt.Mv; f(7)  // (*pt).Mv(7)와 같다
f := t.Mp; f(7)   // (&t).Mp(7)와 같다
f := makeT().Mp   // 허용되지 않음: makeT()의 결괏값의 주소를 취할 수 없다
```

위의 예는 인터페이스가 아닌 타입을 사용하기 하지만, 인터페이스 타입의 값으로 부터 메서드 값을 만드는 것도 허용된다.

```go
var i interface { M(int) } = myVal
f := i.M; f(7)  // i.M(7)와 같다
```
