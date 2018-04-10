# [IncDec 문](#incdec-statements)

"++"과 "--" 문은 피연산자를 미지정 타입 [상수](/Constants/) `1` 만큼 증가시키거나 감소시킨다. 할당문과 마찬가지로, 피연산자는 [주소를 가지고 있거나](/Expressions/address_operators.html) 있거나 map 인덱스 식이어야 한다.

<pre>
<a id="IncDecStmt">IncDecStmt</a> = <a href="/Expressions/operators.html#Expression">Expression</a> ( "++" | "--" ) .
</pre>

아래의 [할당문](/Statements/assignments.html)은 의미상 같은 것이다.

```go
IncDec 문    할당문
x++                 x += 1
x--                 x -= 1
```
