# [메서드 선언](#method-declarations)

메서드는 *리시버*를 동반한 [함수](/Declarations%20and%20scope/function_declarations.html)이다. 메서드 선언은 식별자인, *메서드 이름*을 메서드에 바인딩하고 메서드를 리시버의 *기본 타입*에 연관시킨다.

<pre>
<a id="MethodDecl">MethodDecl</a> = "func" <a href="#Receiver">Receiver</a> <a href="/Types/interface_types.html#MethodName">MethodName</a> ( <a href="/Declarations%20and%20scope/function_declarations.html#Function">Function</a> | <a href="/Types/function_types.html#Signature">Signature</a> ) .
<a id="Receiver">Receiver</a>   = <a href="/Types/function_types.html#Parameters">Parameters</a> .
</pre>

리시버는 메서드 이름 앞에 추가된 매개변수 섹션을 통해 지정된다. 그 매개변수 섹션은 하나의 매개변수인 리시버만을 가지며 가변 매개변수로 지정되어서는 안된다. 그 타입은 (괄호를 사용할 수 있는) `T`나 `*T`의 형식이어야 하고, 이때 `T`는 타입 이름을 나타낸다. `T`로 표시된 타입은 리시버 *기본 타입*이라고 부르고; 포인터나 인터페이스 타입이면 안 되며 메서드와 같은 패키지 안에 [선언되어야](/Declarations%20and%20scope/type_declarations.html)한다. 메서드는 기본 타입에 바인딩 되었다고 말하며 메서드의 이름은 타입 `T` 혹은 `*T`에 대한 [선택자](/Expressions/selectors.html) 표현내 에서만 볼 수 있다.

[blank](/Declarations%20and%20scope/blank_identifier.html) 식별자가 아닌 리시버는 메서드 시그니처내에서  [독특한](/Declarations%20and%20scope/uniqueness_of_identifiers.html)이름이어야 한다. 만약 리시버의 값이 메서드의 본문안에서 참조되지 않았다면, 선언할 때 생략해도 된다. 이와 같은 내용은 함수와 메서드의 매개변수에 일반적으로 함께 적용된다.

어떤 주어진 기본 타입에 바인딩된 메서드의 이름들은 blank 이름이 아닐 때 반드시 독특한 이름을 써야 한다. 만약 기본 타입이 [struct 타입](/Types/struct_types.html)인 경우, blank가 아닌 메서드와 필드 이름들은 서로 달라야 한다.

주어진 `Point` 타입에 대해, 다음의 선언문들은

```go
func (p *Point) Length() float64 {
    return math.Sqrt(p.x * p.x + p.y * p.y)
}

func (p *Point) Scale(factor float64) {
    p.x *= factor
    p.y *= factor
}
```

메서드 `Length`와 `Scale`은 리시버 타입 `*Point`를 통해 기본 타입 `Point`에 바인딩된다.

메서드의 타입은 리시버를 첫번째 인자로 갖는 함수의 타입이다. 예를 들어 메서드 `Scale`의 타입은  

```go
func(p *Point, factor float64)
```

하지만, 함수가 이렇게 선언된 경우는 메서드가 아니다.
