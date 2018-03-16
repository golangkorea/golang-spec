# [break 문](#break-statements)

"break" 문은 같은 함수내 가장 깊은 속의 "[for](/Statements/for_statements.html)", "[switch](/Statements/switch_statements.html)", 혹은 "[select](/Statements/select_statements.html)" 문에 대한 실행을 종료한다.

<pre>
<a id="BreakStmt">BreakStmt</a> = "break" [ <a href="/Statements/labeled_statements.html#Label">Label</a> ] .
</pre>

라벨이 있는 경우에는, 에워싸는 "for", "switch", 혹은 "select" 문에 속해야 하고, 해당 구문은 실행이 종료된다. 

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
