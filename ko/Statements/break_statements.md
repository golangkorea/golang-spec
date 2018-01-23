# Break statements

A "break" statement terminates execution of the innermost "[for](/Statements/for_statements.html)", "[switch](/Statements/switch_statements.html)", or "[select](/Statements/select_statements.html)" statement within the same function.

<pre>
<a id="BreakStmt">BreakStmt</a> = "break" [ <a href="/Statements/labeled_statements.html#Label">Label</a> ] .
</pre>

If there is a label, it must be that of an enclosing "for", "switch", or "select" statement, and that is the one whose execution terminates.

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