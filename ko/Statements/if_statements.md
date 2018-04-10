# [if 문](#if-statements)

"If" 문은 불리언 식의 값에 따라 실행이 결정되는 두 개의 분기를 명시한다. 식이 참으로 평가되면 "if" 분기가 실행되고, 참이 아니고 "else" 분기가 있다면 "else" 분기가 실행된다.

<pre>
<a id="IfStmt">IfStmt</a> = "if" [ <a href="/Statements/#SimpleStmt">SimpleStmt</a> ";" ] <a href="/Expressions/operators.html#Expression">Expression</a> <a href="/Blocks/#Block">Block</a> [ "else" ( <a href="#IfStmt">IfStmt</a> | <a href="/Blocks/#Block">Block</a> ) ] .
</pre>

```go
if x > max {
    x = max
}
```

식 앞에는 간단한 구문이 올 수도 있으며 식이 평가되기 전에 실행된다.

```go
if x := f(); x < y {
    return x
} else if x > z {
    return z
} else {
    return y
}
```
