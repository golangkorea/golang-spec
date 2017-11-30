# Semicolons

# 세미콜론

* spec 버전: of June 28, 2017 
* 원문 : [Semicolons](https://golang.org/ref/spec#Semicolons) 
* 번역자 : [조석규](@ezaurum)


The formal grammar uses semicolons ";" as terminators in a number of productions. Go programs may omit most of these semicolons using the following two rules:

많은 언어에서 세미콜론 ";" 을 종결자로 사용하는 것이 공식적인 문법이다. Go 프로그램은 다음 두 가지 규칙 아래 대부분의 세미콜론을 생략할 수 있다.


1. When the input is broken into tokens, a semicolon is automatically inserted into the token stream immediately after a line's final token if that token is
  + an [identifier](/Lexical elements/identifiers.html)
  + an [integer](/Lexical elements/integer_literals.html), [floating-point](/Lexical elements/floating-point_literals.html), [imaginary](/Lexical elements/imaginary_literals.html), [rune](/Lexical elements/rune_literals.html), or [string](/Lexical elements/string_literals.html) literal
  + one of the [keywords](/Lexical elements/keywords.html) break, continue, fallthrough, or return
  + one of the [operators and delimiters](/Lexical elements/operators_and_delimiters.html) ++, --, ), ], or }
2. To allow complex statements to occupy a single line, a semicolon may be omitted before a closing ")" or "}".

1. 입력이 여러 언어요소로 분리될 때, 언어요소 줄의 마지막 토큰이 다음 두 경우에 해당한다면, 세미콜론은 자동적으로 줄의 가장 끝 바로 뒤에 붙는다.
  + [식별자](/Lexical elements/identifiers.html)
  + [정수](/Lexical elements/integer_literals.html), [부동소수](/Lexical elements/floating-point_literals.html), [허수](/Lexical elements/imaginary_literals.html), [룬](/Lexical elements/rune_literals.html), [문자열](/Lexical elements/string_literals.html) 고정값
2. 복합문이 한 줄만 차지할 수 있도록, 닫는 ")" 나 "}" 앞에서는 세미콜론이 생략될 수 있다.

To reflect idiomatic use, code examples in this document elide semicolons using these rules.

관습적으로 사용될 수 있도록, 이 문서의 코드 예제는 이 규칙에 의거해 세미콜론을 생략했다.
