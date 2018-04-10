# [식 구문](#expression-statements)

일부 내장함수를 제외하고, 구문의 문맥에 함수와 메서드 [호출](/Expressions/calls.html), [수신 연산](/Expressions/receive_operator.html)을 사용할 수 있다. 이런 구문에는 괄호를 사용할 수 있다.

<pre>
<a id="ExpressionStmt">ExpressionStmt</a> = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

다음의 내장 함수는 구문 문맥에 사용할 수 없다.

```go
append cap complex imag len make new real
unsafe.Alignof unsafe.Offsetof unsafe.Sizeof
```

```go
h(x+y)
f.Close()
<-ch
(<-ch)
len("foo")  // len이 내장 함수라면 허용되지 않는다
```
