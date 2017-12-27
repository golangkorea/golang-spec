# [토큰(Tokens)](#tokens)

* Go 버전: 1.9
* 원문 : [Tokens](https://golang.org/ref/spec#Tokens)
* 번역자 : [조석규](@ezaurum)

Tokens form the vocabulary of the Go language. There are four classes: *identifiers*, *keywords*, *operators* and *punctuation*, and *literals*. *White space*, formed from spaces (U+0020), horizontal tabs (U+0009), carriage returns (U+000D), and newlines (U+000A), is ignored except as it separates tokens that would otherwise combine into a single token. Also, a newline or end of file may trigger the insertion of a [semicolon](/Lexical elements/semicolons.html). While breaking the input into tokens, the next token is the longest sequence of characters that form a valid token.

토큰은 Go 언어의 어휘를 형성한다. 토큰에는 *식별자*, *예약어*, *연산자*와 *구두점*, *리터럴*의 네 종류가 있다. 빈칸(U+0020), 가로 탭(U+0009), 캐리지리턴(U+000D), 새 줄(U+000A) 등은 공백 문자이며, 이들은 토큰을 분리할 때를 제외하고 무시된다. 토큰들 사이에 공백 문자가 없으면 하나의 토큰으로 인식된다. 새 줄(U+000A)로 구성된 *공백 문자*는 하나로 뭉쳐질 수 있는 토큰을 분리할 때가 아니면 무시된다. 또, 새 줄이나 파일 끝에[세미콜론](/Lexical elements/semicolons.html)이 추가될 수 있다. 입력을 토큰으로 분리할 때는, 유효한 토큰을 형성하는 가장 긴 연속된 캐릭터들이 다음 토큰이 된다.
