# [룬 리터럴(Rune literals)](#rune-literals)

* Go 버전: 1.9
* 원문 : [Rune literals](https://golang.org/ref/spec#Rune_literals)
* 번역자 : [조석규](@ezaurum)

A rune literal represents a [rune constant](/Constants/), an integer value identifying a Unicode code point. A rune literal is expressed as one or more characters enclosed in single quotes, as in 'x' or '\n'. Within the quotes, any character may appear except newline and unescaped single quote. A single quoted character represents the Unicode value of the character itself, while multi-character sequences beginning with a backslash encode values in various formats.

룬 리터럴은 정수로 된 유니코드 값인 [룬 상수](/Constants/)이다. 룬 리터럴은 `'x'`나 `'\n'`처럼 홑따옴표로 감싸진 한 캐릭터 이상으로 표현된다. 따옴표 안에는 새 줄이나 예외처리되지 않은 홑따옴표 말고는 어떤 캐릭터든 들어갈 수 있다. 홑따옴표로 감싸진 한 캐릭터로 캐릭터 자체의 유니코드 값을 표현할 수 있고, 역슬래시로 시작하는 여러 캐릭터로 값을 부호화하여 표현할 수도 있다.

The simplest form represents the single character within the quotes; since Go source text is Unicode characters encoded in UTF-8, multiple UTF-8-encoded bytes may represent a single integer value. For instance, the literal 'a' holds a single byte representing a literal a, Unicode U+0061, value 0x61, while 'ä' holds two bytes (0xc3 0xa4) representing a literal a-dieresis, U+00E4, value 0xe4.

가장 간단한 형태는 홑따옴표 안에 있는 한 문자인데, Go 소스 코드는 UTF-8으로 부호화된 유니코드 문자로 저장되므로, 하나의 정수값이 UTF-8으로 부호화되어 여러 바이트에 저장될 수 있다. 예를 들어, 리터럴 `'a'`는 리터럴 `a`, 유니코드 U+0061, 값 `0x61`을 1바이트에 저장하지만, `'ä'`는 분음 기호가 붙은 `a`, U+00E4, 값 `0xe4`가 2바이트에 저장된다.

Several backslash escapes allow arbitrary values to be encoded as ASCII text. There are four ways to represent the integer value as a numeric constant: \x followed by exactly two hexadecimal digits; \u followed by exactly four hexadecimal digits; \U followed by exactly eight hexadecimal digits, and a plain backslash \ followed by exactly three octal digits. In each case the value of the literal is the value represented by the digits in the corresponding base.

여러 백슬래시 예외처리가 임의값을 아스키 문자열 형태로 부호화하도록 해 준다. 정수값을 숫자 형태 상수로 표현 할 때는 `\x`뒤에 16진 숫자 두 개, `\u` 뒤에 16진 숫자 네 개, `\U`뒤에 16진 숫자 여덟 개, `\`만 쓰고 그 뒤에 8진 숫자 세 개 를 쓰는 네 가지 방법이 있다. 각각의 형태에서 리터럴은 해당 진수의 숫자값으로 표현된 값이다.

Although these representations all result in an integer, they have different valid ranges. Octal escapes must represent a value between 0 and 255 inclusive. Hexadecimal escapes satisfy this condition by construction. The escapes \u and \U represent Unicode code points so within them some values are illegal, in particular those above 0x10FFFF and surrogate halves.

모든 결과가 정수로 표시되고 있지만, 각각은 유효영역이 다르다. 8진수는 0이상 255이하가 되어야 하고, 16진수는 구조상 이 조건은 만족한다. `\u`와 `\U`는 유니코드 값을 가리키므로 특히 `0x10FFFF` 와 surrogate 영역처럼 유효하지 않은 값이 있다.

After a backslash, certain single-character escapes represent special values:

백슬래시 다음에 한 캐릭터를 붙여 예외처리되는 특별한 값은 다음과 같다.

```
\a   U+0007 alert or bell
\b   U+0008 backspace
\f   U+000C form feed
\n   U+000A line feed or newline
\r   U+000D carriage return
\t   U+0009 horizontal tab
\v   U+000b vertical tab
\\   U+005c backslash
\'   U+0027 single quote  (valid escape only within rune literals)
\"   U+0022 double quote  (valid escape only within string literals)
```

```
\a   U+0007 경고나 비프음
\b   U+0008 백스페이스
\f   U+000C 폼 피드 문자
\n   U+000A 라인 피드 또는 새줄 문자
\r   U+000D 캐리지 리턴
\t   U+0009 수평 탭
\v   U+000b 수직 탭
\\   U+005c 백슬래시
\'   U+0027 홑따옴표 (예외처리는 룬 리터럴 안에서만 가능)
\"   U+0022 겹따옴표 (예외처리는 문자열 리터럴 안에서만 가능)
```

All other sequences starting with a backslash are illegal inside rune literals.

이외에 다른 백슬래시로 지작하는 문자열은 룬 리터럴에 쓸 수 없다.

<pre>
<a id="rune_lit">rune_lit</a>         = "'" ( <a href="#unicode_value">unicode_value</a> | <a href="#byte_value">byte_value</a> ) "'" .
<a id="unicode_value">unicode_value</a>    = <a href="/Source%20code%20representation/characters.html#unicode_char">unicode_char</a> | <a href="#little_u_value">little_u_value</a> | <a href="#big_u_value">big_u_value</a> | <a href="#escaped_char">escaped_char</a> .
<a id="byte_value">byte_value</a>       = <a href="#octal_byte_value">octal_byte_value</a> | <a href="#hex_byte_value">hex_byte_value</a> .
<a id="octal_byte_value">octal_byte_value</a> = `\` <a href="/Source%20code%20representation/letters_and_digits.html#octal_digit">octal_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#octal_digit">octal_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#octal_digit">octal_digit</a> .
<a id="hex_byte_value">hex_byte_value</a>   = `\` "x" <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> .
<a id="little_u_value">little_u_value</a>   = `\` "u" <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> .
<a id="big_u_value">big_u_value</a>      = `\` "U" <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a>
                           <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> .
<a id="escaped_char">escaped_char</a>     = `\` ( "a" | "b" | "f" | "n" | "r" | "t" | "v" | `\` | "'" | `"` ) .
</pre>

```
'a'
'ä'
'本'
'\t'
'\000'
'\007'
'\377'
'\x07'
'\xff'
'\u12e4'
'\U00101234'
'\''         // rune literal containing single quote character
'aa'         // illegal: too many characters
'\xa'        // illegal: too few hexadecimal digits
'\0'         // illegal: too few octal digits
'\uDFFF'     // illegal: surrogate half
'\U00110000' // illegal: invalid Unicode code point
```

```
'a'
'ä'
'本'
'\t'
'\000'
'\007'
'\377'
'\x07'
'\xff'
'\u12e4'
'\U00101234'
'\''         // 홑따옴표 캐릭터의 룬 리터럴
'aa'         // 맞지않음: 캐릭터가 너무 많음
'\xa'        // 맞지않음: 16진수 숫자는 2개 필요
'\0'         // 맞지않음: 8진수 숫자는 3개 필요
'\uDFFF'     // 맞지않음: surrogate 배정 영역
'\U00110000' // 맞지않음: 잘못된 유니코드 값
```
