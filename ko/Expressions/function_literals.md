# [함수 리터럴](#function-literals)

함수 리터럴은 익명 [함수](/Declarationsndcope/function_declarations.html)를 나타낸다.

<pre>
<a id="FunctionLit">FunctionLit</a> = "func" <a href="/Declarations%20and%20scope/function_declarations.html#Function">Function</a> .
</pre>

```go
func(a, b int, z float64) bool { return a*b < int(z) }
```

함수 리터럴은 변수에 할당될 수도 있고 직접 실행될 수도 있다.

```go
f := func(x, y int) int { return x + y }
func(ch chan int) { ch <- ACK }(replyChan)
```

함수 리터럴은 *클로저*이다: 함수 밖에 정의된 변수들을 참조할 수도 있다. 이 변수들은 밖에서 함수 리터럴과 그것을 감싸는 함수사이에서 공유되며, 접근할 수 있는 한 살아 남는다.
