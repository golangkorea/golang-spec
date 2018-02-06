# [세미콜론](#semicolons)

대부분의 Go 문법에서 공식적으로 세미콜론 ";" 을 종결자로 사용한다. Go 프로그램에서는 아래 두 가지 규칙에 따라 세미콜론 대부분을 생략할 수 있다. 

1. 입력이 언어요소로 해석될 때, 줄의 마지막 언어요소가 다음과 같은 경우, 세미콜론이 자동적으로 줄의 가장 끝 바로 뒤에 붙는다.
  + 식별자
  + [정수](/Lexical%20elements/integer_literals.html), [부동소수](/Lexical%20elements/floating-point_literals.html), [허수](/Lexical%20elements/imaginary_literals.html), [룬](/Lexical%20elements/rune_literals.html), [문자열](/Lexical%20elements/string_literals.html) 고정값
  + [예약어](/Lexical%20elements/keywords.html) break, continue, fallthrough, return
  + [연산자와 구두점](/Lexical%20elements/operators_and_punctuation.html) ++, --, ), ], }
2. 복합문이 한 줄에 표시될 수 있도록, ")" 나 "}" 앞에서는 세미콜론이 생략될 수 있다.

Go 코드 작성 관례를 반영해서, 이 문서의 코드 예제는 위 규칙에 따라 세미콜론을 생략했다.
