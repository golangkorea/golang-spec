# [switch 문](#switch-statements)

"switch" 문은 다중 방향 실행을 제공한다. "switch"안에서 식 또는 타입 지정자를 "케이스들"과 비교하여 어느 가지를 실행할 지를 결정한다.

<pre>
<a id="SwitchStmt">SwitchStmt</a> = <a href="#ExprSwitchStmt">ExprSwitchStmt</a> | <a href="#TypeSwitchStmt">TypeSwitchStmt</a> .
</pre>

두가지 형식이 있다: 식 스위치와 타입 스위치. 식 스위치에는, 케이스들이 switch 식의 값과 비교할 식들을 포함한다. 타입 스위치에는, 케이스들이 특별히 주석이 달린 switch 식의 타입과 비교할 타입들을 포함한다. switch 식은 switch 문내에서 정확히 한번 만 평가된다.

## [식 스위치](#expression-switches)

식 스위치에는, switch 식들이 평가되고, 상수일 필요가 없는, 케이스 식들이 왼쪽에서 오른쪽, 그리고 위에서 아래로 평가된다; switch 식과 같은 첫번째가 해당 케이스의 구문들의 실행을 일으킨다; 이외 다른 케이스는 건너뛴다. 일치하는 케이스가 없으며 "기본" 케이스가 있는 경우는 그 케이스의 구문들이 실행된다. 기본 케이스는 오직 하나만 존재해야 하며 "switch" 문안에 아무데나 나타나도 상관없다. switch 식이 없는 경우는 불리언 값 `true`와 동일하다.

<pre>
<a id="ExprSwitchStmt">ExprSwitchStmt</a> = "switch" [ <a href="/Statements/#SimpleStmt">SimpleStmt</a> ";" ] [ <a href="/Expressions/operators.html#Expression">Expression</a> ] "{" { <a href="#ExprCaseClause">ExprCaseClause</a> } "}" .
<a id="ExprCaseClause">ExprCaseClause</a> = <a href="#ExprSwitchCase">ExprSwitchCase</a> ":" <a href="/Blocks/#StatementList">StatementList</a> .
<a id="ExprSwitchCase">ExprSwitchCase</a> = "case" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> | "default" .
</pre>

switch 식이 미지정 타입 상수로 평가되는 경우, 우선 해당 [기본 타입](/Constants/)으로 [변환](/Expressions/conversions.html)된다; 이것이 미지정 불리언 타입인 경우는, 우선 타입 `bool`로 변환된다. 미리 선언된 미지정 타입 값 `nil`은 switch 식으로 사용될 수 없다. 

케이스 식이 타입이 없는 경우, 우선 switch 식의 타입으로 [변환](/Expressions/conversions.html)된다. 각 (이미 변환되었을 지도 모르는) 케이스 식 `x`와 switch 식의 값 `t`에 대해, `x == t`은 정당한 [비교](/Expressions/comparison_operators.html)이어야 한다.

달리 말하자면, switch 문이 명확한 타입없는 임시 변수 `t`를 선언하고 초기화하기 위해 사용되는 것처럼 취급되었다는 말이다; 각 케이스 식 `x`에 대해서 그러한 `t`의 값을 검사해서 등식여부가 결정된다. 

케이스나 기본 절에 있어서, 마지막에 비어있지 않는 구문으로 ([라벨](/Statements/labeled_statements.html)이 붙을 수도 있는) ["fallthrough" 문](/Statements/fallthrough_statements.html)이 올 수 있는데 이것은 제어가 이 절의 마지막에서 다음 절의 첫번째 구문으로 넘어가야 함을 가리킨다. 그렇지 않을 경우 제어는 "switch" 문의 끝으로 넘어간다. "fallthrough" 문은 switch 식의 마지막 절을 제외한 모두의 마지막 구문으로 나타날 수 있다.

switch 식 앞에 간단한 구문이 올 수 있는데, 식이 평가되기 전에 실행된다.

```go
switch tag {
default: s3()
case 0, 1, 2, 3: s1()
case 4, 5, 6, 7: s2()
}

switch x := f(); {  // switch 식이 없으면 "true"를 뜻한다
case x < 0: return -x
default: return x
}

switch {
case x < y: f1()
case x < z: f2()
case x == 4: f3()
}
```

구현시 제한사항: 컴파일러는 다수의 케이스 식들이 같은 상수로 평가되는 것을 허약하지 않을 수 있다. 예를 들어, 현재 구현된 컴파일러들은 똑같은 정수, 부동 소수점, 또는 문자열 상수들을 케이스 식에 허용하지 않는다.

## [타입 스위치](#type-switches)

타입 스위치는 값보다는 타입을 비교한다. 그외에는 식 스위치와 유사하다. 이것은 실제 타입보다는 예약어 `type`을 사용하는 [타입 단언](/Expressions/type_assertions.html)의 형식을 가진 특별한 switch 식으로 구별된다:

```go
switch x.(type) {
// 케이스들
}
```

그리고 케이스들은 실제 타입 `T`를 식 `x`의 동적 타입과 비교한다. 타입 단언과 마찬가지로, `x`는 [인터페이스 타입](/Types/interface_types.html)이어야 하고, 한 케이스내 나열된 각각의 인터페이스 타입이 아닌 `T`는 `x`의 타입을 구현해야 한다. 타입 스위치의 케이스들에 나열된 타입들은 모두 [달라야](/Properties%20of%20types%20and%20values/type_identity.html) 한다.

<pre>
<a id="TypeSwitchStmt">TypeSwitchStmt</a>  = "switch" [ <a href="/Statements/#SimpleStmt">SimpleStmt</a> ";" ] <a href="#TypeSwitchGuard">TypeSwitchGuard</a> "{" { <a href="#TypeCaseClause">TypeCaseClause</a> } "}" .
<a id="TypeSwitchGuard">TypeSwitchGuard</a> = [ <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> ":=" ] <a href="/Expressions/primary_expressions.html#PrimaryExpr">PrimaryExpr</a> "." "(" "type" ")" .
<a id="TypeCaseClause">TypeCaseClause</a>  = <a href="#TypeSwitchCase">TypeSwitchCase</a> ":" <a href="/Blocks/#StatementList">StatementList</a> .
<a id="TypeSwitchCase">TypeSwitchCase</a>  = "case" <a href="#TypeList">TypeList</a> | "default" .
<a id="TypeList">TypeList</a>        = <a href="/Types/#Type">Type</a> { "," <a href="/Types/#Type">Type</a> } .
</pre>

TypeSwitchGuard는 [짧은 변수 선언](/Declarations%20and%20scope/short_variable_declarations.html)을 포함할 수도 있다. 그런 형식이 사용되었을 때는, 각 케이스 절내 [함축적인 블록](/Blocks/)의 출발점에 그 변수가 선언된다. 정확히 하나의 타입을 나열한 케이스의 절에는 변수가 그 타입을 가진다; 그렇지 않은 경우는, 변수가 TypeSwitchGuard내 식의 타입을 가진다.

케이스내 타입은 [nil](/Declarations%20and%20scope/predeclared_identifiers.html)일 수도 있다; 그러한 경우는 TypeSwitchGuard내 식이 `nil` 인터페이스 값일 때 사용된다. `nil` 케이스는 한 개만 허용된다.

타입 `interface{}`을 갖는 주어진 식 `x`에 대해, 다음 타입 스위치는:

```go
switch i := x.(type) {
case nil:
    printString("x is nil")                // i의 타입은 x (interface{})의 타입이다
case int:
    printInt(i)                            // i의 타입은 int이다
case float64:
    printFloat64(i)                        // i의 타입은 float64이다
case func(int) float64:
    printFunction(i)                       // i의 타입은 func(int) float64이다
case bool, string:
    printString("type is bool or string")  // i의 타입은 x (interface{})의 타입이다
default:
    printString("don't know the type")     // i의 타입은x (interface{})의 타입이다
}
```

아래와 같이 고쳐 쓸 수 있다:

```go
v := x  // x는 단 한번만 평가된다
if v == nil {
    i := v                                 // i의 타입은 x (interface{})의 타입이다
    printString("x is nil")
} else if i, isInt := v.(int); isInt {
    printInt(i)                            // i의 타입은 int이다
} else if i, isFloat64 := v.(float64); isFloat64 {
    printFloat64(i)                        // i의 타입은 float64이다
} else if i, isFunc := v.(func(int) float64); isFunc {
    printFunction(i)                       // i의 타입은 func(int) float64이다
} else {
    _, isBool := v.(bool)
    _, isString := v.(string)
    if isBool || isString {
        i := v                         // i의 타입은 x (interface{})의 타입이다
        printString("type is bool or string")
    } else {
        i := v                         // i의 타입은 x (interface{})의 타입이다
        printString("don't know the type")
    }
}
```

타입 스위치 가드(guard) 앞에 간단한 구문이 올 수 있는데, 그럴 경우 가드(guard)가 평가되기 전에 실행된다.

"fallthrough" 문은 타입 스위치안에 사용이 허용되지 않는다.
