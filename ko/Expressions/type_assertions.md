# [타입 단언](#type-assertions)

[인터페시스 타입](/Types/interface_types.html)의 식 `x`과 타입 `T`에 대해, 다음의 기본 식은

```go
x.(T)
```

`x`가 `nil`이 아니고 `x`안에 저장된 값의 타입이 `T`임을 말해준다. `x.(T)`의 표기법은 *타입 단언*이라고 부른다.

더욱 정확하게 말하면, `T`가 인터페이스 타입이 아닐 때, `x.(T)`는 `x`의 동적인 타입이 `T`와 [동일하다](/Propertiesf%20typesnd%20values/type_identity.html)고 말한다. 이 경우, `T`는 `x`의 (인터페이스) 타입을 반드시 [구현](/Types/method_sets.html)해야 한다; 그렇지 않을 경우 `x`가 타입 `T`의 값을 저장할 수 없기 때문에 타입 단언은 유효하지 않다. 만약 `T`가 인터페이스 타입이면, `x.(T)`는 `x`의 동적 타입이 인터페이스 `T`를 구현한다고 말한다.

만약 타입 단언이 유효하면, 식의 값은 `x`안에 저장된 값이고 타입은 `T`이다. 만약 타입 단언이 맞지 않다면, [런타임 패닉](/Run-timeanics/)이 발생한다. 다르게 설명하자면, `x`의 동적 타입을 런타임에서만 알 수 있다해도, 바른 동작을 하는 프로그램에서는 `x.(T)`의 타입이 `T`일 것이라고 알 수 있는 것이다.

```go
var x interface{} = 7          // x는 동적 타입인 int를 가지며 값은 7이다
i := x.(int)                   // i는 타입이 int이며 값이 7이다

type I interface { m() }

func f(y I) {
    s := y.(string)        // 허용되지 않음: string은 I를 구현하지 않는다 (메서드 m이 결여되어 있다)
    r := y.(io.Reader)     // r은 타입 io.Reader을 가지고 y의 동적 타입은 I와 io.Reader 둘 다 구현해야만 한다.
    …
}
```

타입 단언이 [할당문](/Statements/assignments.html)이나 아래와 같은 특별한 형태의 초기화에 사용될 때

```go
v, ok = x.(T)
v, ok := x.(T)
var v, ok = x.(T)
```

추가적으로 미지정 불리언 값을 산출한다. 타입 단언이 유효한 경우 `ok`의 값은 `true`이다. 그렇지 않을 경우에는 `false`이고 `v`의 값은 타입 `T`에 해당하는 [제로 값](/Programnitializationndxecution/the_zero_value.html)이다. 이 경우에 런타임 패닉은 일어나지 않는다.
