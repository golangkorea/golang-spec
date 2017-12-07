# [내장 함수(Built-in functions)](#built-in-functions)

* Go 버전: 1.9
* 원문: [Built-in functions](https://golang.org/ref/spec#Built-in_functions)
* 번역자: Joseph Kim (@superbmilkyway)

Built-in functions are [predeclared](/Declarations%20and%20scope/predeclared_identifiers.html). They are called like any other function but some of them accept a type instead of an expression as the first argument.

내장 함수는 [미리 선언](/Declarations%20and%20scope/predeclared_identifiers.html)되어 있다. 내장 함수는 다른 함수처럼 호출할 수 있지만 몇몇 내장 함수는 식(expression) 대신 타입을 첫 인자로 받는다.

The built-in functions do not have standard Go types, so they can only appear in [call expressions](/Expressions/calls.html); they cannot be used as function values.

내장 함수는 표준 Go 타입을 갖지 않기 때문에 오직 [호출 식](/Expressions/calls.html)에서만 나올 수 있고 함수 값으로는 사용될 수 없다.