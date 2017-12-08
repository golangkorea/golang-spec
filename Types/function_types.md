# [function 타입(Function types)](#function-types)

* Go 버전: 1.9
* 원문: [Function types](https://golang.org/ref/spec#Function_types)
* 번역자: Jhonghee Park (@jhonghee)

A function type denotes the set of all functions with the same parameter and result types. The value of an uninitialized variable of function type is `nil`.

function 타입은 같은 매개변수와 반환 타입을 지닌 모든 함수의 집합을 의미한다. 초기화되지 않은 function 타입의 변수는 `nil` 값을 갖는다.

<pre>
<a id="FunctionType">FunctionType</a>   = "func" <a href="#Signature">Signature</a> .
<a id="Signature">Signature</a>      = <a href="#Parameters">Parameters</a> [ <a href="#Result">Result</a> ] .
<a id="Result">Result</a>         = <a href="#Parameters">Parameters</a> | <a href="/Types/#Type">Type</a> .
<a id="Parameters">Parameters</a>     = "(" [ <a href="#ParameterList">ParameterList</a> [ "," ] ] ")" .
<a id="ParameterList">ParameterList</a>  = <a href="#ParameterDecl">ParameterDecl</a> { "," <a href="#ParameterDecl">ParameterDecl</a> } .
<a id="ParameterDecl">ParameterDecl</a>  = [ <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ] [ "..." ] <a href="/Types/#Type">Type</a> .
</pre>

Within a list of parameters or results, the names (IdentifierList) must either all be present or all be absent. If present, each name stands for one item (parameter or result) of the specified type and all non-[blank](/Declarations%20and%20scope/blank_identifier.html) names in the signature must be [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html). If absent, each type stands for one item of that type. Parameter and result lists are always parenthesized except that if there is exactly one unnamed result it may be written as an unparenthesized type.

매개변수나 반환 값을 표기할 때, 명칭(IdentifierList)은 모두 제공하거나 모두 생략해야 한다. 명칭을 제공할 경우, 각 명칭은 특정 타입을 갖는 1 개의 항목(매개변수 또는 반환 값)을 나타내며, [blank identifier](/Declarations%20and%20scope/blank_identifier.html)를 제외한 모든 명칭은 시그니처 내에서 [고유](/Declarations%20and%20scope/uniqueness_of_identifiers.html)해야 한다. 명칭을 생략한 경우, 나열된 각각의 타입이 해당 항목의 타입을 의미한다. 매개변수와 반환 값 목록은 항상 괄호를 사용해서 묶어주어야 한다. 단, 반환 값이 1 개이고, 이것이 명칭이 주어지지 않은 반환 값(unnamed result)인 경우는 괄호를 생략해도 된다.

The final incoming parameter in a function signature may have a type prefixed with `...`. A function with such a parameter is called *variadic* and may be invoked with zero or more arguments for that parameter.

함수 시그니처의 마지막 매개변수는 타입 정보 앞에 `...`를 함께 사용할 수 있다. 이런 매개 변수를 갖고 있는 함수를 variadic이라고 부르고, 함수 호출시 이 매개변수에 전달되는 인자가 여러 개일 수도 있고, 하나도 없을 수도 있다.

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