# [부동소수점 리터럴(Floating-point literals)](#floating-point-literals)

* Go 버전: 1.9
* 원문 : [Floating-point literals](https://golang.org/ref/spec#Floating-point_literals)
* 번역자 : [조석규](@ezaurum)

A floating-point literal is a decimal representation of a [floating-point constant](/Constants/). It has an integer part, a decimal point, a fractional part, and an exponent part. The integer and fractional part comprise decimal digits; the exponent part is an e or E followed by an optionally signed decimal exponent. One of the integer part or the fractional part may be elided; one of the decimal point or the exponent may be elided.

부동 소수점 리터럴은 [부동 소수점 상수](/Constants/)의 십진수 표현이다. 정수부, 소수점, 소수부, 지수부로 구성된다. 정수부와 소수부는 십진수이고 지수부는 `e`나 `E`뒤에 붙는 부호가 있을 수 있는 십진수이다. 정수부나 소수부 중 하나, 아니면 소수점이나 지수부 중 하나는 생략가능하다.

<pre>
<a id="float_lit">float_lit</a> = <a href="#decimals">decimals</a> "." [ <a href="#decimals">decimals</a> ] [ <a href="#exponent">exponent</a> ] |
            <a href="#decimals">decimals</a> <a href="#exponent">exponent</a> |
            "." <a href="#decimals">decimals</a> [ <a href="#exponent">exponent</a> ] .
<a id="decimals">decimals</a>  = <a href="/Source%20code%20representation/letters_and_digits.html#decimal_digit">decimal_digit</a> { <a href="/Source%20code%20representation/letters_and_digits.html#decimal_digit">decimal_digit</a> } .
<a id="exponent">exponent</a>  = ( "e" | "E" ) [ "+" | "-" ] <a href="#decimals">decimals</a> .
</pre>

```
0.
72.40
072.40  // == 72.40
2.71828
1.e+0
6.67428e-11
1E6
.25
.12345E+5
```
