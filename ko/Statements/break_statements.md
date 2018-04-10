# [break 문](#break-statements)

"break" 문은 같은 함수 안에서 break 문과 가장 가까이 있는 "[for](/Statements/for_statements.html)", "[switch](/Statements/switch_statements.html)", "[select](/Statements/select_statements.html)" 문에 대한 실행을 종료한다.

<pre>
<a id="BreakStmt">BreakStmt</a> = "break" [ <a href="/Statements/labeled_statements.html#Label">Label</a> ] .
</pre>

라벨이 있는 경우에는, "for", "switch", "select" 문 내부에 break 문이 있어야 하며, 라벨과 함께 사용된  break 구문은 실행을 종료시킨다.

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
