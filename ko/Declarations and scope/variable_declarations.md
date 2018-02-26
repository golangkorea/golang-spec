# [변수 선언](#variable-declarations)

변수 선언은 하나 이상의 [변수](/Variables/)를 만들어, 상응하는 식별자를 바인딩하고, 각각에 타입과 초기값을 준다.

<pre>
<a id="VarDecl">VarDecl</a>     = "var" ( <a href="#VarSpec">VarSpec</a> | "(" { <a href="#VarSpec">VarSpec</a> ";" } ")" ) .
<a id="VarSpec">VarSpec</a>     = <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ( <a href="/Types/#Type">Type</a> [ "=" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> ] | "=" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> ) .
</pre>

```go
var i int
var U, V, W float64
var k = 0
var x, y float32 = -1, -2
var (
    i       int
    u, v, s = 2.0, 3.0, "bar"
)
var re, im = complexSqrt(-1)
var _, found = entries[name]  // 맵을 조회; "found"만을 원한다.
```

표현식의 리스트가 주어졌을때, 변수는 [할당](/Statements/assignments.html) 규칙을 따르는 표현식으로 초기화된다. 그외 경우는 각 변수들이 [제로 값](/Program%20initialization%20and%20execution/the_zero_value.html)으로 초기화된다.

만약 타입이 제시되었다면, 각 변수에 그 타입이 주어진다. 그렇지 않을 경우, 각 변수에는 할당시에 상응하는 초기값의 타입이 주어진다. 만약 값이 미지정 타입 상수일 경우는 우선 [초기 타입](/Constants/)으로 [변환](/Expressions/conversions.html) 한다; 미지정 불리언 값의 경우, 우선 타입 `bool`로 변환된다. 미리 선언된 값인 `nil`은 명백한 타입이 없는 변수를 초기화하는데 사용될 수 없다.

```go
var d = math.Sin(0.5)  // d 는 float64
var i = 42             // i 는 int
var t, ok = x.(T)      // t 는 T, ok 는 bool
var n = nil            // 허용않됨
```

구현시 제한사항: 컴파일러는 만약 변수가 사용되지 않았다면 [함수 본문](/Declarations%20and%20scope/function_declarations.html)안에서 그 변수가 선언되는 것을 허용하지 않을 수도 있다.
