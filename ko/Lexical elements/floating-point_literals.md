# [Floating-point literals](#floating-point-literals)

A floating-point literal is a decimal representation of a [floating-point constant](/Constants/). It has an integer part, a decimal point, a fractional part, and an exponent part. The integer and fractional part comprise decimal digits; the exponent part is an e or E followed by an optionally signed decimal exponent. One of the integer part or the fractional part may be elided; one of the decimal point or the exponent may be elided.

<pre><a id="float_lit">float_lit</a> = <a href="#decimals">decimals</a> "." [ <a href="#decimals">decimals</a> ] [ <a href="#exponent">exponent</a> ] |
            <a href="#decimals">decimals</a> <a href="#exponent">exponent</a> |
            "." <a href="#decimals">decimals</a> [ <a href="#exponent">exponent</a> ] .
<a id="decimals">decimals</a>  = <a href="/Source%20code%20representation/letters_and_digits.html#decimal_digit">decimal_digit</a> { <a href="/Source%20code%20representation/letters_and_digits.html#decimal_digit">decimal_digit</a> } .
<a id="exponent">exponent</a>  = ( "e" | "E" ) [ "+" | "-" ] <a href="#decimals">decimals</a> .
</pre>