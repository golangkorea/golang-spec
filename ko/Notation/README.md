# [표기법](#notation)

문법은 Extended Backus-Naur Form (EBNF)를 사용해 명시된다:

```go
Production  = production_name "=" [ Expression ] "." .
Expression  = Alternative { "|" Alternative } .
Alternative = Term { Term } .
Term        = production_name | token [ "…" token ] | Group | Option | Repetition .
Group       = "(" Expression ")" .
Option      = "[" Expression "]" .
Repetition  = "{" Expression "}" .
```

생성규칙은 용어들과 다음의 연산자들로 부터 우선 순위가 높은 순서대로 만들어진 표현식이다.

```go
|   alternation
()  grouping
[]  option (0이나 1번)
{}  repetition (0이나 n번)
```

어휘적인 토큰을 식별하기 위해 소문자로 구성된 생성규칙의 이름이 사용된다. 비말단기호는 케멀케이스로 표현된다. 어휘적인 토큰들은 큰 따옴표 `""`나 역 따옴표 <code>``</code>안에 묶는다.

`a … b`의 형식은 `a`에서 `b`까지의 문자 집합을 선택할 수 있는 대안 문자들로 나타낸다. 또 수평 줄임표 `…`는 스펙문서의 다른 곳들에서 다양한 열거나 생략하는 코드 조각들을 나타내는데 비 공식적으로 사용된다. `…` 문자는 (세 문자인 ... 에 반하여) Go 언어의 토큰이 아니다.
