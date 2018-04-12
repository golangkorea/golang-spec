# [continue 문](#continue-statements)

"continue"문은 자신을 에워싸고 있는 가장 가까운 ["for" 루프](/Statements/for_statements.html)의 post 구문에서 루프의 다음 반복을 시작한다. "for" 루프는 동일한 함수 안에 있어야 한다.

<pre>
<a id="ContinueStmt">ContinueStmt</a> = "continue" [ <a href="/Statements/labeled_statements.html#Label">Label</a> ] .
</pre>

continue 문에 라벨이 있는 경우 continue문을 에워싸는 for문의 라벨이어야 하며, 해당 for 문의 다음 단계로 실행을 진행시킨다.

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
