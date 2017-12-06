# [소스 코드 표현(Source code representation)](#source-code-representation)

* Go 버전: 1.9
* 원문: [Source code representation](https://golang.org/ref/spec#Source_code_representation)
* 번역자: Sang-joon, Moon(@dakeshi)

Source code is Unicode text encoded in [UTF-8](http://en.wikipedia.org/wiki/UTF-8). The text is not canonicalized, so a single accented code point is distinct from the same character constructed from combining an accent and a letter; those are treated as two code points. For simplicity, this document will use the unqualified term *character* to refer to a Unicode code point in the source text.

소스코드는 [UTF-8](http://en.wikipedia.org/wiki/UTF-8)로 인코드된 유니코드 문자다. 이 문자는 정규화되지(canonicalized) 않았기 때문에, 같은 문자라도 악센트, 글자의 조합으로 구성된 문자와 1개의 악센트 코드 포인트(code point)는 같지 않다; 즉, 이들은 2 개의 코드 포인트로 인식된다. 이 문서에서는 소스코드에서 유니코드 코드 포인트를 언급할 때  *캐릭터(character)*라는 용어를 사용할 것이다.      

Each code point is distinct; for instance, upper and lower case letters are different characters.

각각의 코드 포인트는 고유하다; 예를 들어, 같은 문자라도 대문자, 소문자는 다른 캐릭터로 취급한다.  

Implementation restriction: For compatibility with other tools, a compiler may disallow the NUL character (U+0000) in the source text.

구현 제한: 다른 도구와의 호환성을 위해, 컴파일러는 소스코드에서 NUL 캐릭터(U+0000) 사용하는 것을 허용하지 않을 수 있다.

Implementation restriction: For compatibility with other tools, a compiler may ignore a UTF-8-encoded byte order mark (U+FEFF) if it is the first Unicode code point in the source text. A byte order mark may be disallowed anywhere else in the source.

구현 제한: 다른 도구와의 호환성을 위해, 컴파일러는 소스코드에서 첫 번째 유니코드 코드 포인트가 UTF-8로 인코드된 바이트 오더 마크(byte order mark, U+FEFF)라면 이를 무시할 것이다. 바이트 오더 마크는 소스코드에서 허용되지 않을 수 있다.
