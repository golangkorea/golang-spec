# [선택자](#selectors)

[패키지 이름](/Packages/package_clause.html)이 아닌 [기본 식](/Expressions/primary_expressions.html) `x`에 대하여, 다음과 같은 *선택자 표현식*은

```go
x.f
```

`x` 값(때로는 `*x`; 아래 참조)의 필드 또는 메서드 `f`를 뜻한다. 식별자 `f`는 (필드 혹은 메서드) *선택자*라고 불린다; [blank 식별자](/Declarationsndcope/blank_identifier.html)가 아니여야 한다. 선택자 표현식의 타입은 `f`의 타입이다. `x`가 패키지 이름일 경우, [한정적 식별자](/Expressions/qualified_identifiers.html) 섹션을 참고하라.

선택자 `f`는 타입 `T`의 필드나 메서드 `f`를 뜻할 수도 있고, `T`의 중첩된 [임베드된 필드](/Types/struct_types.html)의 필드나 메서드 `f`를 참조할 수도 있다. `f`까지 도달하는데 드는 임베드된 필드의 수를 `T`안의 *깊이*라고 부른다. `T`안에 선언된 필드나 메서드 `f`의 깊이는 0 이다. `T`안에 임베드된 필드 `A`속에 선언된 필드나 메서드 `f`의 깊이는 `A`안의 `f`의 깊이 더하기 1 이다.

선택자에는 다음의 규칙들이 적용된다:

  * `T`가 포인터도 아니고 인터페이스 타입도 아닌 경우의 타입 `T` 혹은 `*T`의 값 `x`에 대해, `f`가 존재하는 경우 `x.f`는 `T`내 가장 얕은 깊이에 위치한 필드나 메서드를 뜻한다. 만약 가장 얕은 깊이에 정확히 [단 하나의 `f`](/Declarations%20and%20scope/uniqueness_of_identifiers.html)만 존재하는 것이 아니라면, 그런 선택자 표현식은 허용되지 않는다.
  * `I`가 인터페이스 타입인 경우 타입 `I`의 값 `x`에 대해, `x.f`는 `x`의 동적인 값의 `f`라는 이름을 갖는 실제 메서드를 뜻한다. 만약 `I`의 [메서드 집합](/Types/method_sets.html)내 `f`라는 이름의 메서드가 없다면, 그런 선택자 표현식은 허용되지 않는다.
  * 한가지 예외로, 만약 `x`의 타입이 이름이 주어진 포인터 타입이고 `(*x).f`가 (메서드가 아닌) 필드를 뜻하는 유효한 선택자 표현식이라면, `x.f`는 `(*x).f`를 속기한 형태이다.
  * 이 외 다른 모든 경우에, `x.f`는 허용되지 않는다.
  * 만약 `x`가 포인터 타입이고 `nil` 값을 가지고 있으며 `x.f`가 구조체의 필드를 의미하는 경우에, `x.f`에 할당하거나 그것을 평가하는 일은 [런타입 패닉](/Run-time%20panics/)을 일으킨다.
  * 만약 `x`가 인터페이스 타입이고 `nil` 값을 가지고 있다면, 메서드 `x.f`를 [호출하거나](/Expressions/calls.html) [평가하는 것](/Expressions/method_values.html)은 [런타입 패닉](/Run-time%20panics/)을 일으킨다.

예를 들어, 주어진 선언문들에서:

```go
type T0 struct {
    x int
}

func (*T0) M0()

type T1 struct {
    y int
}

func (T1) M1()

type T2 struct {
    z int
    T1
    *T0
}

func (*T2) M2()

type Q *T2

var t T2     // with t.T0 != nil
var p *T2    // with p != nil and (*p).T0 != nil
var q Q = p
```

다음과 같이 작성할 수 있다:

```go
t.z          // t.z
t.y          // t.T1.y
t.x          // (*t.T0).x

p.z          // (*p).z
p.y          // (*p).T1.y
p.x          // (*(*p).T0).x

q.x          // (*(*q).T0).x        (*q).x는 유효한 필드 선택자이다

p.M0()       // ((*p).T0).M0()      M0는 *T0 리시버를 예상한다
p.M1()       // ((*p).T1).M1()      M1은 T1 리시버를 예상한다
p.M2()       // p.M2()              M2는 *T2 리시버를 예상한다
t.M2()       // (&t).M2()           M2는 *T2 리시버를 예상한다, 호출에 대한 섹션을 참조.
```

하지만 다음은 유효하지 않다:

```go
q.M0()       // (*q).M0는 유효하지만 필드 선택자는 아니다
```
