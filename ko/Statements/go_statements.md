# [go 문](#go-statements)

"go" 문은 같은 주소 공간 안에 고루틴(goroutine)이라 불리는 별도로 제어되는 독립적인 동시성 쓰레드 형태로 함수 호출의 실행을 시작한다.

<pre>
<a id="GoStmt">GoStmt</a> = "go" <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

식(expression)은 함수 또는 메서드 호출이어야 한다; 괄호는 허용되지 않는다. 일부 내장 함수는 식에 사용할 수 없으며, 해당 내장 함수 목록은 [식 구문](/Statements/expression_statements.html) 챕터를 참고하라.

고루틴 호출시 함수 값과 매개 변수들은 [평소처럼 평가되지만](/Expressions/calls.html), 프로그램 실행이 호출된 함수가 완료될 때까지 기다리지 않는다는 점에서 일반적인 호출과 차이가 있다. 대신, 고루틴에 의해 호출된 함수는 새로운 고루틴에서 독립적으로 실행을 시작한다. 함수가 종료되면 고루틴도 함께 종료된다. 반환 값이 있는 함수라면 함수가 완료될 때 이들 반환 값은 제거된다.

```go
go Server()
go func(ch chan<- bool) { for { sleep(10); ch <- true }} (c)
```
