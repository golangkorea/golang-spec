# [캐릭터](#characters)

다음의 용어들은 특정한 유니코드 캐릭터 분류를 나타내기 위해 사용 되었다.

<pre>
<a id="newline">newline</a>        = /* 유니코드 포인트 U+000A */ .
<a id="unicode_char">unicode_char</a>   = /* newline을 제외한 임의의 유니코드 포인트 */ .
<a id="unicode_letter">unicode_letter</a> = /* "Letter"로 분류된 유니코드 포인트 */ .
<a id="unicode_digit">unicode_digit</a>  = /* "Number, decimal digit"로 분류된 유니코드 포인트 */ .
</pre>

[유니코드 표준 8.0](http://www.unicode.org/versions/Unicode8.0.0/)내, 섹션 4.5 "일반적 카테고리"는 캐릭터 카테고리의 집합을 정의한다. Go는 Letter 카테고리들인 Lu, Ll, Lt, Lm, 혹은 Lo에 속하는 모든 캐릭터를 유니코드 알파벳 문자로 취급하고 Number 카테고리인 Nd에 속한 것들은 유니코드 숫자들로 취급한다.
