# [부동소수점 리터럴](#floating-point-literals)

부동 소수점 리터럴은 [부동 소수점 상수](/Constants/)의 십진수 표현이다. 정수부, 소수점, 소수부, 지수부로 구성된다. 정수부와 소수부는 십진수이고 지수부는 `e`나 `E`뒤에 붙는 부호가 있을 수 있는 십진수이다. 정수부나 소수부 중 하나, 아니면 소수점이나 지수부 중 하나는 생략가능하다.

<pre>
<a id="float_lit">float_lit</a> = <a href="#decimals">decimals</a> "." [ <a href="#decimals">decimals</a> ] [ <a href="#exponent">exponent</a> ] |
            <a href="#decimals">decimals</a> <a href="#exponent">exponent</a> |
            "." <a href="#decimals">decimals</a> [ <a href="#exponent">exponent</a> ] .
<a id="decimals">decimals</a>  = <a href="/Source%20code%20representation/letters_and_digits.html#decimal_digit">decimal_digit</a> { <a href="/Source%20code%20representation/letters_and_digits.html#decimal_digit">decimal_digit</a> } .
<a id="exponent">exponent</a>  = ( "e" | "E" ) [ "+" | "-" ] <a href="#decimals">decimals</a> .
</pre>

```go
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
