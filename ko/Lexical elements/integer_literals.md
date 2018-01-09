# [Integer literals](#integer-literals)

An integer literal is a sequence of digits representing an integer [constant](/Constants/). An optional prefix sets a non-decimal base: 0 for octal, 0x or 0X for hexadecimal. In hexadecimal literals, letters a-f and A-F represent values 10 through 15.

<pre>
<a id="int_lit">int_lit</a>     = <a href="#decimal_lit">decimal_lit</a> | <a href="#octal_lit">octal_lit</a> | <a href="#hex_lit">hex_lit</a> .
<a id="decimal_lit">decimal_lit</a> = ( "1" … "9" ) { <a href="/Source%20code%20representation/letters_and_digits.html#decimal_digit">decimal_digit</a> } .
<a id="octal_lit">octal_lit</a>   = "0" { <a href="/Source%20code%20representation/letters_and_digits.html#octal_digit">octal_digit</a> } .
<a id="hex_lit">hex_lit</a>     = "0" ( "x" | "X" ) <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> { <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> } .
</pre>

    42
    0600
    0xBadFace
    170141183460469231731687303715884105727