# Integer literals

An integer literal is a sequence of digits representing an integer constant. An optional prefix sets a non-decimal base: 0 for octal, 0x or 0X for hexadecimal. In hexadecimal literals, letters a-f and A-F represent values 10 through 15.

<pre>
<a id="int_lit">int_lit</a>     = decimal_lit | octal_lit | hex_lit .
<a id="decimal_lit">decimal_lit</a> = ( "1" … "9" ) { decimal_digit } .
<a id="octal_lit">octal_lit</a>   = "0" { octal_digit } .
<a id="hex_lit">hex_lit</a>     = "0" ( "x" | "X" ) hex_digit { hex_digit } .
</pre>

```
42
0600
0xBadFace
170141183460469231731687303715884105727
```