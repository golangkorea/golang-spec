# [함수 리터럴](#function-literals)

함수 리터럴은 익명 [함수](/Declarationsndcope/function_declarations.html)를 나타낸다.

<pre>
<a id="FunctionLit">FunctionLit</a> = "func" <a href="/Declarations%20and%20scope/function_declarations.html#Function">Function</a> .
</pre>

```go
func(a, b int, z float64) bool { return a*b < int(z) }
```

함수 리터럴을 변수에 할당할 수도 있고 직접 실행할 수도 있다.

```go
f := func(x, y int) int { return x + y }
func(ch chan int) { ch <- ACK }(replyChan)
```

함수 리터럴은 *클로저* 다: 함수 리터럴이 포함되어 있는 서라운딩 함수(surrounding function)에 정의된 변수를 함수 리터럴에서 참조할 수 있다. 이 변수들은 함수 리터럴과 서라운딩 함수가 공유하며 이들 함수에 접근할 수 있다면 이 변수들을 사용할 수 있다.
