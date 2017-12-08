# [식별자(Identifiers)](#identifiers)

* Go 버전: 1.9
* 원문: [Identifiers](https://golang.org/ref/spec#Identifiers)
* 번역자: [조석규](@ezaurum)

Identifiers name program entities such as variables and types. An identifier is a sequence of one or more letters and digits. The first character in an identifier must be a letter.

식별자는 변수나 타입같은 프로그램 구성 요소에 이름을 붙인다. 식별자는 한 자 이상의 연속된 영문자와 숫자이다. 식별자의 첫자는 영문자여야만 한다.

<pre>
<a id="identifier">identifier</a> = <a href="/Source code representation/letters_and_digits.html#letter">letter</a> { <a href="/Source code representation/letters_and_digits.html#letter">letter</a> | <a href="/Source code representation/characters.html#unicode_digit">unicode_digit</a> } .
</pre>

```
a
_x9
ThisVariableIsExported
αβ
```

Some identifiers are [predeclared](/Declarations and scope/predeclared_identifiers.html).

식별자는 [미리 선언](/Declarations and scope/predeclared_identifiers.html) 될 수 있다.
