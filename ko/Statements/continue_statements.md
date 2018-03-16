# [continue 문](#continue-statements)

"continue" 문은 구문 바로 뒤의 위치에서 가장 깊숙한 ["for" 루프](/Statements/for_statements.html)의 다음 반복을 시작한다. "for" 루프는 동일한 함수내 있어야 한다.

<pre>
<a id="ContinueStmt">ContinueStmt</a> = "continue" [ <a href="/Statements/labeled_statements.html#Label">Label</a> ] .
</pre>

라벨이 있는 경우, 에워싸는 "for" 문에 속해야 하고, 그 구문의 실행이 전진하게 된다.

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
