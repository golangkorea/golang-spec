# [식 구문](#expression-statements)

명시된 내장함수를 제외하고, 함수와 메서드 [호출](/Expressions/calls.html) 그리고 [수신 연산](/Expressions/receive_operator.html)은 구문의 맥락안에 나타날 수 있다. 그러한 구문들에는 괄호를 사용할 수 있다.

<pre>
<a id="ExpressionStmt">ExpressionStmt</a> = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

다음의 내장 함수들은 구문 맥락에서 사용이 허락되지 않는다.

```go
append cap complex imag len make new real
unsafe.Alignof unsafe.Offsetof unsafe.Sizeof
```

```go
h(x+y)
f.Close()
<-ch
(<-ch)
len("foo")  // 만약 len이 내장 함수라면 허용되지 않는다
```
