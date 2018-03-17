# [goto 문](#goto-statements)

"goto" 문은 같은 함수내 라벨이 붙은 구문으로 제어를 이전한다.

<pre>
<a id="GotoStmt">GotoStmt</a> = "goto" <a href="/Statements/labeled_statements.html#Label">Label</a> .
</pre>

```go
goto Error
```

"goto" 문을 실행했을 때 goto가 있던 시점의 범위 안에 없던 변수가 도입되는 일이 없어야 한다. 예를 들어, 다음의 예제는:

```go
    goto L  // 잘못된 사용
    v := 3
L:
```

라벨 `L`로 점프하면서 `v`의 생성을 건너뛰게 되어 오류를 발생시킬 수 있다.

한 [블록](/Blocks/)의 외부에 있는 "goto" 문은 그 블록안에 있는 라벨로 점프할 수 없다. 예를 들어, 다음 예제는:

```go
if n%2 == 1 {
    goto L1
}
for n > 0 {
    f()
    n--
L1:
    f()
    n--
}
```

"for" 문안에 라벨 `L1`이 있지만 `goto`는 없게 때문에 오류를 발생시킬 수 있다.
