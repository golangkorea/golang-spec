# [주석(Comments)](#comments)

* Go 버전: 1.9
* 원문: [Comments](https://golang.org/ref/spec#Comments)
* 번역자: Sang-joon, Moon(@dakeshi)

Comments serve as program documentation. There are two forms:

1. *Line comments* start with the character sequence // and stop at the end of the line.
2. *General comments* start with the character sequence /\* and stop with the first subsequent character sequence \*/.

주석을 이용해 프로그램 문서화를 할 수 있다. 주석은 2가지 형태가 있다:

1. *라인 주석*은 //로 시작하며 라인 끝에서 끝난다.
2. *일반 주석*은 /\*로 시작해서 \*/을 처음 만났을 때 끝난다. 

A comment cannot start inside a [rune](/Lexical elements/rune_literals.html) or [string literal](/Lexical elements/string_literals.html), or inside a comment. A general comment containing no newlines acts like a space. Any other comment acts like a newline. 

주석은 [룬 문자](/Lexical elements/rune_literals.html), [문자열 리터럴](/Lexical elements/string_literals.html) 또는 주석 내부에서 시작할 수 없다. newline이 없는 일반 주석은 공백(space)처럼 동작하며, 그 밖의 주석은 newline처럼 동작한다.