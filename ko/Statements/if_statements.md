# [if 문](#if-statements)

"If" 문은 불리언 식의 값에 따라 결정되는 두개의 실행 가지를 조건적인 실행을 명시한다. 만약 식이 참으로 평가되면, "if" 가지가 실행되고, 거짓이면, "else" 가지가 있는 경우 실행된다.

<pre>
<a id="IfStmt">IfStmt</a> = "if" [ <a href="/Statements/#SimpleStmt">SimpleStmt</a> ";" ] <a href="/Expressions/operators.html#Expression">Expression</a> <a href="/Blocks/#Block">Block</a> [ "else" ( <a href="#IfStmt">IfStmt</a> | <a href="/Blocks/#Block">Block</a> ) ] .
</pre>

```go
if x > max {
    x = max
}
```

식앞에 간단한 구문이 올 수도 있는데, 그럴 경우 식이 평가되기 전에 실행된다.

```go
if x := f(); x < y {
    return x
} else if x > z {
    return z
} else {
    return y
}
```
