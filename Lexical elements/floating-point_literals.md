# Floating-point literals

A floating-point literal is a decimal representation of a [floating-point constant](/Constatns/). It has an integer part, a decimal point, a fractional part, and an exponent part. The integer and fractional part comprise decimal digits; the exponent part is an e or E followed by an optionally signed decimal exponent. One of the integer part or the fractional part may be elided; one of the decimal point or the exponent may be elided.

<pre>
<a id="float_lit">float_lit</a> = decimals "." [ decimals ] [ exponent ] |
            decimals exponent |
            "." decimals [ exponent ] .
<a id="decimals">decimals</a>  = decimal_digit { decimal_digit } .
<a id="exponent">exponent</a>  = ( "e" | "E" ) [ "+" | "-" ] decimals .
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