# [Imaginary literals](#imaginary-literals)

An imaginary literal is a decimal representation of the imaginary part of a [complex constant](/Constants/). It consists of a floating-point literal or decimal integer followed by the lower-case letter i.

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