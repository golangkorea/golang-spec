# Tokens

# 언어요소

spec 버전: of June 28, 2017
원문 : [Tokens](https://golang.org/ref/spec#Tokens)
번역자 : [조석규](@ezaurum)

Tokens form the vocabulary of the Go language.

언어요소는 Go 언어의 어휘를 형성한다.

There are four classes: *identifiers*, *keywords*, *operators* and *delimiters*, and *literals*.
 
언어요소에는 *식별자*, *예약어*, *연산자*와 *구분자*, *고정값* 네 종류가 있다.

*White space*, formed from spaces (U+0020), horizontal tabs (U+0009), carriage returns (U+000D), and newlines (U+000A), is ignored except as it separates tokens that would otherwise combine into a single token.

빈칸(U+0020), 가로 탭(U+0009), 캐리지리턴(U+000D), 새 줄(U+000A)으로 구성된 *공백 문자*는 하나로 뭉쳐질 수 있는 언어요소를 분리할 때가 아니면 무시된다.

Also, a newline or end of file may trigger the insertion of a [semicolon](/Lexical elements/semicolons.html).

또, 새 줄이나 파일 끝에[세미콜론](/Lexical elements/semicolons.html)이 추가될 수 있다.

While breaking the input into tokens, the next token is the longest sequence of characters that form a valid token.

입력을 언어요소로 분리할 때는, 유효한 언어요소를 형성하는 가장 긴 연속된 문자열이 다음 언어요소가 된다.
