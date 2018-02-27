# [메서드 식](#method-expressions)

타입 `T`의 [메서드 집합](/Types/method_sets.html)안에 `M`이 있으면, `T.M`은 보통 함수처럼 호출할 수 있는데, 이때 `M`과 같은 인자들에 추가로 메서드의 리시버가 앞에 붙는다.

<pre>
<a id="MethodExpr">MethodExpr</a>    = <a href="#ReceiverType">ReceiverType</a> "." <a href="/Types/interface_types.html#MethodName">MethodName</a> .
<a id="ReceiverType">ReceiverType</a>  = <a href="/Types/#TypeName">TypeName</a> | "(" "*" <a href="/Types/#TypeName">TypeName</a> ")" | "(" <a href="#ReceiverType">ReceiverType</a> ")" .
</pre>

2개의 메서드를 가지고 있는 struct 타입 `T`를 검토해 보자. `Mv` 메서드는 리시버의 타입이 `T`이고, `Mp` 메서드는 리시버의 타입이 `*T`이다.

```go
type T struct {
    a int
}
func (tv  T) Mv(a int) int         { return 0 }  // 리시버가 값인 경우
func (tp *T) Mp(f float32) float32 { return 1 }  // 리시버가 포인터인 경우

var t T
```

다음과 같은 식은

```go
T.Mv
```

`Mv`와 동등한 함수를 생산하지만 첫번째 인자로 명시적인 리시버를 가지며; 다음과 같은 시그니처를 갖고 있다.

```go
func(tv T, a int) int
```

이 함수는 명시적인 리시버를 사용해 정상적으로 호출될 수 있어서, 다음과 같이 5개의 실행방식은 동등하다:

```go
t.Mv(7)
T.Mv(t, 7)
(T).Mv(t, 7)
f1 := T.Mv; f1(t, 7)
f2 := (T).Mv; f2(t, 7)
```

유사하게, 다음과 같은 식은

```go
(*T).Mp
```

아래와 같은 시그니처를 갖는 `Mp`를 대표하는 함수 값을 생산한다.

```go
func(tp *T, f float32) float32
```

리시버가 값인 메서드에 대해서, 명시적인 포인터 리시버를 갖는 함수를 유도해 낼 수 있어서

```go
(*T).Mv
```

는 아래의 시그니처를 갖는 `Mv`를 대표하는 함수 값을 생산한다.

```go
func(tv *T, a int) int
```

이러한 함수는 리시버를 통해 간접적으로 값을 만들어서 내재하는 메서드에 리시버로 전달한다; 이 메서드는 함수 호출에서 주소가 전달된 값을 겹쳐쓰지 않는다.

마지막 케이스인 포인터-리시버 메서드에 대한 값-리시버 함수는 포인터-리시버 메서드가 값의 타입이 갖고 있는 메서드 집합에 포함되지 않기 때문에 허용되지 않는다.

메서드로 부터 파생된 함수 값들은 함수 호출 문법을 통해 호출된다; 리시버가 첫번째 인자로 호출에 제공된다. 즉, 주어진 `f := T.Mv`에 대해, `f`는 `f(t, 7)`로 실행되며 `t.f(7)`로 실행되지 않는다. 리시버를 바인딩하는 함수를 만들려면, [함수 리터럴](/Expressions/function_literals.html)이나 [메서드 값](/Expressions/method_values.html)을 사용하라.

인터페이스 타입의 메서드로 부터 함수 값을 파생시키는 것은 허용된다. 결과적으로 얻는 함수는 그 인터페이스 타입의 명시적인 리시버를 받아 들인다.
