# [Rune literals](#rune-literals)

A rune literal represents a [rune constant](/Constants/), an integer value identifying a Unicode code point. A rune literal is expressed as one or more characters enclosed in single quotes, as in 'x' or '\n'. Within the quotes, any character may appear except newline and unescaped single quote. A single quoted character represents the Unicode value of the character itself, while multi-character sequences beginning with a backslash encode values in various formats.

The simplest form represents the single character within the quotes; since Go source text is Unicode characters encoded in UTF-8, multiple UTF-8-encoded bytes may represent a single integer value. For instance, the literal 'a' holds a single byte representing a literal a, Unicode U+0061, value 0x61, while 'ä' holds two bytes (0xc3 0xa4) representing a literal a-dieresis, U+00E4, value 0xe4.

Several backslash escapes allow arbitrary values to be encoded as ASCII text. There are four ways to represent the integer value as a numeric constant: \x followed by exactly two hexadecimal digits; \u followed by exactly four hexadecimal digits; \U followed by exactly eight hexadecimal digits, and a plain backslash \ followed by exactly three octal digits. In each case the value of the literal is the value represented by the digits in the corresponding base.

Although these representations all result in an integer, they have different valid ranges. Octal escapes must represent a value between 0 and 255 inclusive. Hexadecimal escapes satisfy this condition by construction. The escapes \u and \U represent Unicode code points so within them some values are illegal, in particular those above 0x10FFFF and surrogate halves.

After a backslash, certain single-character escapes represent special values:

```
\a   U+0007 alert or bell
\b   U+0008 backspace
\f   U+000C form feed
\n   U+000A line feed or newline
\r   U+000D carriage return
\t   U+0009 horizontal tab
\v   U+000b vertical tab
\\   U+005c backslash
\'   U+0027 single quote  (valid escape only within rune literals)
\"   U+0022 double quote  (valid escape only within string literals)
```

All other sequences starting with a backslash are illegal inside rune literals.

<pre>
<a id="rune_lit">rune_lit</a>         = "'" ( <a href="#unicode_value">unicode_value</a> | <a href="#byte_value">byte_value</a> ) "'" .
<a id="unicode_value">unicode_value</a>    = <a href="/Source%20code%20representation/characters.html#unicode_char">unicode_char</a> | <a href="#little_u_value">little_u_value</a> | <a href="#big_u_value">big_u_value</a> | <a href="#escaped_char">escaped_char</a> .
<a id="byte_value">byte_value</a>       = <a href="#octal_byte_value">octal_byte_value</a> | <a href="#hex_byte_value">hex_byte_value</a> .
<a id="octal_byte_value">octal_byte_value</a> = `\` <a href="/Source%20code%20representation/letters_and_digits.html#octal_digit">octal_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#octal_digit">octal_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#octal_digit">octal_digit</a> .
<a id="hex_byte_value">hex_byte_value</a>   = `\` "x" <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> .
<a id="little_u_value">little_u_value</a>   = `\` "u" <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> .
<a id="big_u_value">big_u_value</a>      = `\` "U" <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a>
                           <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> <a href="/Source%20code%20representation/letters_and_digits.html#hex_digit">hex_digit</a> .
<a id="escaped_char">escaped_char</a>     = `\` ( "a" | "b" | "f" | "n" | "r" | "t" | "v" | `\` | "'" | `"` ) .
</pre>

```
'a'
'ä'
'本'
'\t'
'\000'
'\007'
'\377'
'\x07'
'\xff'
'\u12e4'
'\U00101234'
'\''         // rune literal containing single quote character
'aa'         // illegal: too many characters
'\xa'        // illegal: too few hexadecimal digits
'\0'         // illegal: too few octal digits
'\uDFFF'     // illegal: surrogate half
'\U00110000' // illegal: invalid Unicode code point
```
