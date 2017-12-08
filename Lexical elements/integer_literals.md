# [정수 리터럴(Integer literals)](#integer-literals)

* Go 버전: 1.9
* 원문 : [Integer literals](https://golang.org/ref/spec#Integer_literals)
* 번역자 : [조석규](@ezaurum)

An integer literal is a sequence of digits representing an integer [constant](/Constants/). An optional prefix sets a non-decimal base: 0 for octal, 0x or 0X for hexadecimal. In hexadecimal literals, letters a-f and A-F represent values 10 through 15.

정수 리터럴은 [정수 상수](/Constants/)를 표현하는 연속된 숫자이다. 십진수가 아닌 경우 접두사가 붙을 수 있다. `0`은 8진수, `0x`나 `0X`는 16진수이다. 16진수 리터럴의 경우 영문자 `a-f`와 `A-F`가 10에서 15를 표현한다.

<pre>
<a id="int_lit">int_lit</a>     = <a href="#decimal_lit">decimal_lit</a> | <a href="#octal_lit">octal_lit</a> | <a href="#hex_lit">hex_lit</a> .
<a id="decimal_lit">decimal_lit</a> = ( "1" … "9" ) { <a href="/Source%20code%20representation/letters_and_digits.html#decimal_digit">decimal_digit</a> } .
<a id="octal_lit">octal_lit</a>   = "0" { <a href="/Source%20code%20representation/letters_and_digits.html#octal_digit">octal_digit</a> } .
<a id="hex_lit">hex_lit</a>     = "0" ( "x" | "X" ) <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> { <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> } .
</pre> 

```
42
0600
0xBadFace
170141183460469231731687303715884105727
```
