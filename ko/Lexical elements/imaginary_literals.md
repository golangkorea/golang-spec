# [허수 리터럴](#imaginary-literals)

허수 리터럴은 [복소 상수](/Constants/)에서 허수부를 십진수로 나타낸 것이다. 소문자 `i` 뒤에 [부동소수점 리터럴](/Lexical elements/floating-point_literals.html)이나 십진 정수가 붙은 형태이다.

<pre>
<a id="imaginary_lit">imaginary_lit</a> = (<a href="/Lexical%20elements/floating-point_literals.html#decimals">decimals</a> | <a href="/Lexical%20elements/floating-point_literals.html#float_lit">float_lit</a>) "i" .
</pre>

```go
0i
011i  // == 11i
0.i
2.71828i
1.e+0i
6.67428e-11i
1E6i
.25i
.12345E+5i
```
