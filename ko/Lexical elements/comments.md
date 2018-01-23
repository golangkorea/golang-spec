# [주석](#comments)

주석을 이용해 프로그램 문서화를 할 수 있다. 주석은 2가지 형태가 있다:

1. *라인 주석*은 //로 시작하며 라인 끝에서 끝난다.
2. *일반 주석*은 /\*로 시작해서 \*/을 처음 만났을 때 끝난다. 

주석은 [룬 문자](/Lexical elements/rune_literals.html), [문자열 리터럴](/Lexical elements/string_literals.html) 또는 주석 내부에서 시작할 수 없다. newline이 없는 일반 주석은 공백(space)처럼 동작하며, 그 밖의 주석은 newline처럼 동작한다.