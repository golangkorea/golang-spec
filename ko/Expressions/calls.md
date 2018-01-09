# 호출

함수 타입 F의 식 f 에 대해서

```go
f(a1, a2, … an)
```

f를 인자a1, a2, … an 로 호출한다. 특별한 경우 하나를 제외하고, 인자는 매개변수 타입에 [할당 가능](/Statements/assignments.html)해야 하고, 값이 하나로 나오는 식이어야 하며, 호출 직전에 평가된다. 식의 타입은 F의 결과 타입이다. 메소드 호출은, 메소드 리시버 타입의 선택자의 값이 메소드 자체로 지정되는 것 말고는 비슷하다.

```go
math.Atan2(x, y)  // function call
var pt *Point
pt.Scale(3.5)     // method call with receiver pt
```

함수 호출에서, 함수값과 인자들은 [보통 순서](/Expressions/order_of_evaluation.html)로 평가된다. 평가된 다음, 호출의 매개변수는 값으로 함수에 전달되고, 함수가 실행된다. 함수의 반환 매개변수는 함수가 반환 될 때 호출한 함수에 값으로 전달된다.

`nil`인 함수값을 호출하면 [run-time panic](/Run-time%20panics/)이 유발된다.

특별한 경우로, 메서드 또는 함수 g의 반환 값이 다른 함수 또는 메서드 f의 매개 변수와 같은 갯수이고 개별적으로 할당가능 하다면, f (g (*parameters_of_g*)) 와 같은 호출은 g의 반환값을 f 의 매개변수에 순서대로 바인딩하여 호출될 것이다. f가 호출 될 때, g의 호출 이외의 다른 매개변수가 있어서는 안 되고, g는 최소한 하나의 반환값이 있어야 한다. 만일 함수 f의 마지막 매개변수에 ...가 있다면, 만일 함수 f의 마지막 매개변수에 ...가 있다면, g의 반환값 중 보통 매개변수에 할당되고 난 다음 값들이 할당된다.

```go
func Split(s string, pos int) (string, string) {
    return s[0:pos], s[pos:]
}

func Join(s, t string) string {
    return s + t
}

if Join(Split(value, len(value)/2)) != value {
    log.Panic("test fails")
}
```

메서드 호출 x.m()는 x 타입의 [메서드 집합](/Types/method_sets.html)에 m이 있고, 인수 목록이 m의 매개 변수 목록에 할당할 수 있을 때 유효하다. x가 [주소 지정이 가능하고](/Expressions/address_operators.html) &x의 메서드 집합에 m이 있다면, (&x).m()를 x.m()로 줄여쓸 수 있다.

```go
var p Point
p.Scale(3.5)
```

따로 구분되는 메소드 타입이나 메소드 리터럴은 없다.