# [메서드 식](#method-expressions)

`M`이 타입 `T`의 [메서드 집합](/Types/method_sets.html) 중 하나라면, `T.M`은 같은 인자를 가진 일반적인 함수처럼 호출할 수 있는 함수이며, 이때 `M` 뒤에는 추가적인 인자인 메서드의 수신자(receiver)가 위치한다.

<pre>
<a id="MethodExpr">MethodExpr</a>    = <a href="#ReceiverType">ReceiverType</a> "." <a href="/Types/interface_types.html#MethodName">MethodName</a> .
<a id="ReceiverType">ReceiverType</a>  = <a href="/Types/#TypeName">TypeName</a> | "(" "*" <a href="/Types/#TypeName">TypeName</a> ")" | "(" <a href="#ReceiverType">ReceiverType</a> ")" .
</pre>

2개의 메서드가 있는 struct 타입 `T` 에서 `Mv` 메서드는 `T` 타입의 수신자, `Mp` 메서드는 `*T` 타입의 수신자를 가지고 있다.

```go
type T struct {
    a int
}
func (tv  T) Mv(a int) int         { return 0 }  // 값 수신자
func (tp *T) Mp(f float32) float32 { return 1 }  // 포인터 수신자

var t T
```

아래 식은

```go
T.Mv
```

명시적으로 수신자를 첫번째 인자로 가진다는 차이만 있을 뿐 `Mv` 와 동일한 함수가 된다; 이 함수의 시그니처는 다음과 같다.

```go
func(tv T, a int) int
```

이 함수는 명시적으로 수신자를 사용해 정상적으로 호출할 수 있기 때문에, 아래의 5개 호출은 같은 것이다:

```go
t.Mv(7)
T.Mv(t, 7)
(T).Mv(t, 7)
f1 := T.Mv; f1(t, 7)
f2 := (T).Mv; f2(t, 7)
```

유사하게, 이 식은

```go
(*T).Mp
```

아래와 같은 시그니처를 가진 `Mp`를 나타내는 함수 값(function value)이 된다.

```go
func(tp *T, f float32) float32
```

값 수신자를 가진 메서드는 명시적으로 포인터 수신자를 가진 함수를 제공할 수 있기 때문에

```go
(*T).Mv
```

는 아래의 시그니처를 가진 `Mv`를 나타내는 함수 값이 된다.

```go
func(tv *T, a int) int
```

이러한 함수는 내재 메서드에 대한 수신자처럼 전달할 값을 생성하기 위해 수신자를 통해 참조된다; 이 메서드는 함수 호출에서 전달된 주소에 있는 값을 겹쳐쓰지 않는다.

마지막으로 포인터 수신자를 가진 메서드에 대한 값 수신자 함수는 허용되지 않는다. 그 이유는 포인터 수신자 메서드가 값 타입의 메서드 집합에 포함되어 있지 않기 때문이다. 

메서드로부터 파생된 함수 값들은 함수 호출 문법을 통해 호출된다; 호출시 수신자가 첫번째 인자로 제공된다. 즉, `f := T.Mv`에 대해, `f`는 `t.f(7)` 가 아니라 `f(t, 7)` 와 같은 형태로 호출된다. 수신자와 관련된 함수를 만들려면, [함수 리터럴](/Expressions/function_literals.html)이나 [메서드 값](/Expressions/method_values.html)을 사용하라.

인터페이스 타입의 메서드에서 함수 값을 만드는 것은 허용된다. 그 결과로 나오는 함수는 해당 인터페이스 타입의 명시적인 수신자를 인자로 갖는다.
