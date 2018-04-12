# [break 문](#break-statements)

"break" 문은 자신을 에워싸고 있는 가장 가까운 "[for](/Statements/for_statements.html)", "[switch](/Statements/switch_statements.html)", "[select](/Statements/select_statements.html)" 문에 대한 실행을 종료한다.

<pre>
<a id="BreakStmt">BreakStmt</a> = "break" [ <a href="/Statements/labeled_statements.html#Label">Label</a> ] .
</pre>

break 문에 라벨이 있는 경우, break 문을 에워싸는 "for", "switch", "select" 문의 라벨이어야 하며, 해당 구문의 실행을 종료시킨다.


```go
OuterLoop:
    for i = 0; i < n; i++ {
        for j = 0; j < m; j++ {
            switch a[i][j] {
            case nil:
                state = Error
                break OuterLoop
            case item:
                state = Found
                break OuterLoop
            }
        }
    }
```
