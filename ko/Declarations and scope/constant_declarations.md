# [상수 선언](#constant-declarations)

상수 선언은 식별자들(상수들의 이름)의 목록을 [상수 표현식]([Expressions/constant_expressions.html) 목록의 값들과 결합한다. 식별자의 개수는 반드시 표현식의 개수와 일치해야 하며, 좌측에 있는 n번째 식별자는 우측에 있는 n번째 표현식의 값과 결합된다.

<pre>
<a id="ConstDecl">ConstDecl</a>      = "const" ( <a href="#ConstSpec">ConstSpec</a> | "(" { <a href="#ConstSpec">ConstSpec</a> ";" } ")" ) .
<a id="ConstSpec">ConstSpec</a>      = <a href="#IdentifierList">IdentifierList</a> [ [ <a href="/Types/#Type">Type</a> ] "=" <a href="#ExpressionList">ExpressionList</a> ] .

<a id="IdentifierList">IdentifierList</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> { "," <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> } .
<a id="ExpressionList">ExpressionList</a> = <a href="/Expressions/operators.html#Expression">Expression</a> { "," <a href="/Expressions/operators.html#Expression">Expression</a> } .
</pre>

타입이 있는 경우, 모든 상수들은 타입이 지정되며, 그 표현식은 해당 타입에 반드시 [할당 가능](/Properties%20of%20types%20and%20values/assignability.html)해야 한다. 타입이 생략된다면, 상수는 해당하는 표현식의 타입을 개별적으로 갖는다. 만약 표현식 값들이 미지정 타입 [상수](/Constants/)라면, 선언된 상수들은 미지정 타입으로 남게 되고 상수 식별자들은 상수 값들로 표현된다. 예를 들어 표현식이 부동 소수점 리터럴인 경우, 상수 식별자는 이 리터럴의 실수부가 0이라고 하더라도 부동 소수점 상수로 표현된다.

```go
const Pi float64 = 3.14159265358979323846
const zero = 0.0         // 미지정 타입의 부동 소수점 상수
const (
    size int64 = 1024
    eof        = -1  // 미지정 타입의 정수 상수
)
const a, b, c = 3, 4, "foo"  // a = 3, b = 4, c = "foo", 미지정 타입의 정수와 문자열 상수
const u, v float32 = 0, 3    // u = 0.0, v = 3.0
```

괄호로 묶인 상수 선언 목록 내에서의 표현식 목록은 첫 번째 선언을 제외하고는 모두 생략될 수 있다. 이러한 빈 목록은 앞에서 처음 나타나는 비어있지 않은 표현식 목록이 있다면 그 타입의 텍스트 치환과 동일하다. 따라서 표현식의 목록을 생략하는 것은 이전 목록을 반복하는 것과 동일하다. 이 경우, 식별자들의 개수는 이전 목록 내에서의 표현식의 개수와 동일해야 한다. 이 메커니즘은 [iota 상수 제너레이터](/Declarations%20and%20scope/iota.html)와 함께 사용되어 연속된 값들의 선언을 손쉽게 할 수 있도록 한다.:

```go
const (
    Sunday = iota
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Partyday
    numberOfDays  // 이 상수는 내보내지지 않는다.
)
```
