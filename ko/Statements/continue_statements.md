# Continue statements

A "continue" statement begins the next iteration of the innermost ["for" loop](/Statements/for_statements.html) at its post statement. The "for" loop must be within the same function.

<pre>
<a id="ContinueStmt">ContinueStmt</a> = "continue" [ <a href="/Statements/labeled_statements.html#Label">Label</a> ] .
</pre>

If there is a label, it must be that of an enclosing "for" statement, and that is the one whose execution advances.

```go
RowLoop:
    for y, row := range rows {
        for x, data := range row {
            if data == endOfRow {
                continue RowLoop
            }
            row[x] = data + bias(x, y)
        }
    }
```