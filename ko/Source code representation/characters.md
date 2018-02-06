# Characters

The following terms are used to denote specific Unicode character classes:

<pre>
<a id="newline">newline</a>        = /* the Unicode code point U+000A */ .
<a id="unicode_char">unicode_char</a>   = /* an arbitrary Unicode code point except newline */ .
<a id="unicode_letter">unicode_letter</a> = /* a Unicode code point classified as "Letter" */ .
<a id="unicode_digit">unicode_digit</a>  = /* a Unicode code point classified as "Number, decimal digit" */ .
</pre>

In [The Unicode Standard 8.0](http://www.unicode.org/versions/Unicode8.0.0/), Section 4.5 "General Category" defines a set of character categories. Go treats all characters in any of the Letter categories Lu, Ll, Lt, Lm, or Lo as Unicode letters, and those in the Number category Nd as Unicode digits.
