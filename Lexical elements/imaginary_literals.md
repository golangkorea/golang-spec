# [허수 리터럴(Imaginary literals)](#imaginary-literals)

* Go 버전: 1.9
* 원문 : [Imaginary literals](https://golang.org/ref/spec#Imaginary_literals)
* 번역자 : [조석규](@ezaurum)

An imaginary literal is a decimal representation of the imaginary part of a [complex constant](/Constants/). It consists of a floating-point literal or decimal integer followed by the lower-case letter i.

허수 리터럴은 [복소 상수](/Constants/)에서 허수부를 십진수로 나타낸 것이다. 소문자 `i` 뒤에 [부동소수점 리터럴](/Lexical elements/floating-point_literals.html)이나 십진 정수가 붙은 형태이다.

<pre>
<a id="imaginary_lit">imaginary_lit</a> = (<a href="/Lexical%20elements/floating-point_literals.html#decimals">decimals</a> | <a href="/Lexical%20elements/floating-point_literals.html#float_lit">float_lit</a>) "i" .
</pre>

```
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
