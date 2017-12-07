# [세미콜론(Semicolons)](#semicolons)

* Go 버전: 1.9
* 원문 : [Semicolons](https://golang.org/ref/spec#Semicolons) 
* 번역자 : [조석규](@ezaurum)


The formal grammar uses semicolons ";" as terminators in a number of productions. Go programs may omit most of these semicolons using the following two rules:

1. When the input is broken into tokens, a semicolon is automatically inserted into the token stream immediately after a line's final token if that token is
  + an [identifier](/Lexical elements/identifiers.html)
  + an [integer](/Lexical elements/integer_literals.html), [floating-point](/Lexical elements/floating-point_literals.html), [imaginary](/Lexical elements/imaginary_literals.html), [rune](/Lexical elements/rune_literals.html), or [string](/Lexical elements/string_literals.html) literal
  + one of the [keywords](/Lexical elements/keywords.html) break, continue, fallthrough, or return
  + one of the [operators and punctuation](/Lexical elements/operators_and_punctuation.html) ++, --, ), ], or }
2. To allow complex statements to occupy a single line, a semicolon may be omitted before a closing ")" or "}".

대부분의 Go 문법에서 공식적으로 세미콜론 ";" 을 종결자로 사용한다. Go 프로그램에서는 아래 두 가지 규칙에 따라 세미콜론 대부분을 생략할 수 있다. 

1. 입력이 언어요소로 해석될 때, 줄의 마지막 언어요소가 다음과 같은 경우, 세미콜론이 자동적으로 줄의 가장 끝 바로 뒤에 붙는다.
  + [식별자](/Lexical elements/identifiers.html)
  + [정수](/Lexical elements/integer_literals.html), [부동소수](/Lexical elements/floating-point_literals.html), [허수](/Lexical elements/imaginary_literals.html), [룬](/Lexical elements/rune_literals.html), [문자열](/Lexical elements/string_literals.html) 고정값
  + [예약어](/Lexical elements/keywords.html) break, continue, fallthrough, return
  + [연산자와 구두점](/Lexical elements/operators_and_punctuation.html) ++, --, ), ], }
2. 복합문이 한 줄에 표시될 수 있도록, ")" 나 "}" 앞에서는 세미콜론이 생략될 수 있다.

To reflect idiomatic use, code examples in this document elide semicolons using these rules.

Go 코드 작성 관례를 반영해서, 이 문서의 코드 예제는 위 규칙에 따라 세미콜론을 생략했다.
