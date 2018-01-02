# [문자열 리터럴](#string-literals)

문자열 리터럴은 연속한 캐릭터를 서로 이어서 만든 [문자열 상수](/Constants/)이다. 비가공 문자열 리터럴과 가공 문자열 리터럴의 두 가지가 있다.

비가공 문자열 리터럴은 `foo`처럼 강세표 사이에 있는 연속된 캐릭터이다. 강세표 사이에는 강세표를 제외하고 어떤 캐릭터든 올 수 있다. 비가공 문자열 리터럴은 암시적으로 UTF-8으로 부호화된, 번역되지 않은 캐릭터로 구성된 문자열이다. 백슬래시는 아무 의미가 없고, 새 줄 문자도 들어갈 수 있다. 캐리지 리턴 캐릭터('\r')는 버려진다.

가공 문자열 리터럴은 `"bar"` 처럼 겹따옴표 사이에 있는 연속된 캐릭터이다. 겹따옴표 사이에는 새 줄 문자와 예외처리 되지 않은 겹따옴표를 제외하고 어떤 캐릭터든 올 수 있다. 따옴표 사이의 문자가 리터럴이 되게 되는데, [rune literals](/Lexical%20elements/rune_literals.html)과 동일하게(\'는 쓸 수 없고 \" 는 쓸 수 있다) 백슬래시로 예외처리된다. 세자리 8진수(\nnn) 와 두 자리 16진수(\xnn)는 결과 문자열의 각 바이트로 번역된다. 그 이외의 모든 예외처리는 개별 캐릭터가 (여러 바이트에 걸쳐질 수 있는) UTF-8으로 부호화된 형태를 의미한다. 그러므로 문자열 리터럴에서 `\377`과 `xFF`는 한 바이트 값 `0xFF`=255 이고, `ÿ`, `\u00FF`, `\U000000FF`, `\xc3\xbf`는 문자 U+00FF가 UTF-8으로 부호화된 두 바이트를 의미한다.

<pre>
<a id="string_lit">string_lit</a>             = <a href="#raw_string_lit">raw_string_lit</a> | <a href="#interpreted_string_lit">interpreted_string_lit</a> .
<a id="raw_string_lit">raw_string_lit</a>         = "`" { <a href="/Source%20code%20representation/characters.html#unicode_char">unicode_char</a> | <a href="/Source%20code%20representation/characters.html#newline">newline</a> } "`" .
<a id="interpreted_string_lit">interpreted_string_lit</a> = `"` { <a href="/Lexical%20elements/rune_literals.html#unicode_value">unicode_value</a> | <a href="/Lexical%20elements/rune_literals.html#byte_value">byte_value</a> } `"` .
</pre>

```
`abc`                // "abc"와 동일
`\n
\n`                  // "\\n\n\\n" 와 동일
"\n"
"\""                 //  `"` 와 동일
"Hello, world!\n"
"日本語"
"\u65e5本\U00008a9e"
"\xff\u00FF"
"\uD800"             // 맞지않음: surrogate 배정 영역
"\U00110000"         // 맞지않음: 잘못된 유니코드 코드 포인트
```

아래 예는 모두 같은 문자열을 표현한 것이다.

```
"日本語"                                 // UTF-8 입력 문자열
`日本語`                                 // UTF-8 비가공 문자열 리터럴
"\u65e5\u672c\u8a9e"                    // 명시적인 유니코드 코드 포인트
"\U000065e5\U0000672c\U00008a9e"        // 명시적인 유니코드 코드 포인트
"\xe6\x97\xa5\xe6\x9c\xac\xe8\xaa\x9e"  // 명시적인 유니코드 바이트값
```

만일 소스코드가 강세표와 한 영문자를 포함하는 형태 같이 두 개 코드 포인트를 하나의 캐릭터에 넣으려고 한다면, 룬 리터럴에 넣을 때는 하나의 코드 포인트가 아니므로 에러가 나고, 문자열 리터럴에 넣을 때는 두 개 코드값으로 나타날 것이다.