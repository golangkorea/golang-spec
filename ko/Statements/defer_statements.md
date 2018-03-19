# [defer 문](#defer-statements)

"defer" 문은 서라운딩 함수가 리턴되는 시점에 지연되었던 함수를 호출한다. 서라운딩 함수가 리턴되는 시점은 서라운딩 함수가 [return 문](/Statements/return_statements.html)을 실행했거나, 서라운딩 함수의 [함수 본문](/Declarations%20and%20scope/function_declarations.html) 끝에 도달했거나, 서라운딩 함수와 관련된 고루틴(goroutine)이 [패닉킹](/Built-in%20functions/handling_panics.html)인 경우다.

<pre>
<a id="DeferStmt">DeferStmt</a> = "defer" <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

식(expression)은 함수 또는 메서드 호출이어야 한다; 괄호는 허용되지 않는다. 일부 내장 함수는 식에 사용할 수 없으며, 이들의 목록은 [식 구문](/Statements/expression_statements.html) 챕터를 참고하라.

"defer" 문이 실행될 때마다, 호출에 대한 함수 값과 매개변수들은 [평소처럼 평가되고](/Expressions/calls.html) 새롭게 저장되지만, 실제 함수는 호출되지 않는다. 대신, 지연된 함수들은 지연된 순서의 역순으로 서라운딩 함수가 리턴되기 직전에 호출된다. 지연된 함수 값이 `nil` 로 평가되면 "defer" 문이 실행될 때가 아니라 함수가 호출될 때 실행이 [패닉](/Built-in%20functions/handling_panics.html)된다.

예를 들어, 지연된 함수가 [함수 리터럴](/Expressions/function_literals.html) 이고 서라운딩 함수가 [이름이 있는 결과 파라미터](/Types/function_types.html)이며, 이들 파라미터가 리터럴 내부 범위에 있다면, 지연된 함수는 결과 파라미터를 리턴하기 전에 이들을 접근, 수정할 수 있다. 지연된 함수가 리턴 값을 가지고 있다면, 이들은 함수가 완료될 때 제거된다. (추가 정보는 [패닉 처리](/Built-in%20functions/handling_panics.html) 챕터를 확인하세요.)

```go
lock(l)
defer unlock(l)  // 서라운딩 함수가 리턴되기 전에 unlock이 일어난다.

// 서라운딩 함수가 리턴되기 전에 3 2 1 0 이 출력된다.
for i := 0; i <= 3; i++ {
    defer fmt.Print(i)
}

// f 는 1을 리턴한다.
func f() (result int) {
    defer func() {
        result++
    }()
    return 0
}
```
