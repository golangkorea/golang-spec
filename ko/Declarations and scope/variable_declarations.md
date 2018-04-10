# [변수 선언문](#variable-declarations)

변수 선언문은 하나 이상의 [변수](/Variables/)를 만들어 상응하는 식별자와 연결하고, 각 변수에 타입과 초기값을 설정한다.

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
var _, found = entries[name]  // map 에서 관심있는 "found"만 조회한다.
```

식(expression)의 리스트가 주어졌을때,  [할당](/Statements/assignments.html) 규칙을 따르는 식으로 변수는 초기화된다. 그밖의 경우는 각 변수들이 [제로 값](/Program%20initialization%20and%20execution/the_zero_value.html)으로 초기화된다.

타입이 명시된 경우 각 변수는 해당 타입으로 설정된다.  그렇지 않은 경우, 각 변수는 할당시 초기값에 해당하는 타입으로 설정된다. 값이 미지정 타입 상수라면, 우선 [기본 타입](/Constants/)으로 [변환](/Expressions/conversions.html) 된다; 미지정 타입의 불리언 값인 경우 우선 `bool` 타입으로 변환된다. 미리 선언된 값인 `nil`은 명백한 타입이 없는 변수를 초기화하는데 사용할 수 없다.

```go
var d = math.Sin(0.5)  // d 는 float64
var i = 42             // i 는 int
var t, ok = x.(T)      // t 는 T, ok 는 bool
var n = nil            // 허용안됨
```

구현시 제한사항: 컴파일러는 사용하지 않는 변수를 [함수 본문](/Declarations%20and%20scope/function_declarations.html)안에서 선언하는 것을 허용하지 않을 수 있다.
