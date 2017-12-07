# [함수 타입(Function types)](#function-types)

 * Go 버전: 1.9
 * 원문: [Function types](https://golang.org/ref/spec#Function_types)
 * 번역자: Jhonghee Park (@jhonghee)

A function type denotes the set of all functions with the same parameter and result types. The value of an uninitialized variable of function type is `nil`.

함수 타입은 동일한 매개변수와 반환 타입을 지닌 모든 함수의 집합을 의미한다. 함수 타입의 초기화되지 않은 변수의 값은 `nil`이다.

<pre>
<a id="FunctionType">FunctionType</a>   = "func" <a href="#Signature">Signature</a> .
<a id="Signature">Signature</a>      = <a href="#Parameters">Parameters</a> [ <a href="#Result">Result</a> ] .
<a id="Result">Result</a>         = <a href="#Parameters">Parameters</a> | <a href="/Types/#Type">Type</a> .
<a id="Parameters">Parameters</a>     = "(" [ <a href="#ParameterList">ParameterList</a> [ "," ] ] ")" .
<a id="ParameterList">ParameterList</a>  = <a href="#ParameterDecl">ParameterDecl</a> { "," <a href="#ParameterDecl">ParameterDecl</a> } .
<a id="ParameterDecl">ParameterDecl</a>  = [ <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ] [ "..." ] <a href="/Types/#Type">Type</a> .
</pre>

Within a list of parameters or results, the names (IdentifierList) must either all be present or all be absent. If present, each name stands for one item (parameter or result) of the specified type and all non-[blank](/Declarations%20and%20scope/blank_identifier.html) names in the signature must be [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html). If absent, each type stands for one item of that type. Parameter and result lists are always parenthesized except that if there is exactly one unnamed result it may be written as an unparenthesized type.

매개 변수나 반환 값들의 리스트내에서, 명칭들(IdentifierList)은 모두 나타나 있던지 아니면 아예 없어야 한다. 만약 모두 있다면, 각 명칭들은 주어진 타입의 한 항목(매개변수 혹은 반환값)을 나타내고 시그니처(signature)내의 모든 비-[공백(blank)](/Declarations%20and%20scope/blank_identifier.html) 명칭들은 [독특해야](/Declarations%20and%20scope/uniqueness_of_identifiers.html) 한다. 만약 모든 명칭이 부재인 경우는, 각 타입이 그 타입의 한 항목임을 나타낸다. 매개변수와 반환 값 리스트는 항상 괄호를 사용해서 묶어 주어야 한다. 예외로 명칭이 주어지지 않은 반환 값이 단 하나일 때 괄호를 생략해도 된다.

The final incoming parameter in a function signature may have a type prefixed with .... A function with such a parameter is called *variadic* and may be invoked with zero or more arguments for that parameter.

함수의 시그니처내 맨 마지막에 오는 매개 변수는 ...을 앞세운 타입을 가질 수도 있다. 이런 매개 변수를 갖고 있는 함수를 *가변성(variadic)*이라고 부르고 그 매개변수를 위해 0 보다 크거나 같은 수의 인자를 사용해서 호출할 수 있다.

```
func()
func(x int) int
func(a, _ int, z float32) bool
func(a, b int, z float32) (bool)
func(prefix string, values ...int)
func(a, b int, z float64, opt ...interface{}) (success bool)
func(int, int, float64) (float64, *[]int)
func(n int) func(p *T)
```