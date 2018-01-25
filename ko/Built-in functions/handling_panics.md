# [패닉 처리](#handling-panics)

두 내장 함수인 `panic`과 `recover`는 [런타임 패닉](/Run-time panics/)과 프로그램에서 정의된  오류 조건들의 제어 및 보고를 돕는다.

```go
func panic(interface{})
func recover() interface{}
```

func panic(interface{})func recover() interface{}함수 `F`를 실행하는 동안에, 명시적인 `panic` 호출이나 [런타임 패닉](/Run-time panics/)은 `F`의 실행을 중단시킨다. 그 뒤에 `F`가 [지연](/Statements/defer_statements.html)시킨 모든 함수들은 평상시와 같이 실행된다. 그 다음, `F`의 호출자가 수행하는 모든 지연된 함수들이 실행되고, 이런 식으로 이어져서 실행 중인 고루틴의 최상위 함수에 의해 지연된 모든 함수들이 실행된다. 그 시점에서, 프로그램이 종료되면서 `panic`에 인자로 주어진 값을 포함하는 오류 상태가 보고된다. 이러한 종료 절차를 *패닉킹*이라고 부른다.

```go
panic(42)
panic("unreachable")
panic(Error("cannot parse"))
```

The `recover` function allows a program to manage behavior of a panicking goroutine. Suppose a function `G` defers a function `D` that calls `recover` and a panic occurs in a function on the same goroutine in which `G` is executing. When the running of deferred functions reaches `D`, the return value of `D`'s call to `recover` will be the value passed to the call of `panic`. If `D` returns normally, without starting a new `panic`, the panicking sequence stops. In that case, the state of functions called between `G` and the call to `panic` is discarded, and normal execution resumes. Any functions deferred by `G` before `D` are then run and `G`'s execution terminates by returning to its caller.

The return value of `recover` is `nil` if any of the following conditions holds:

  * `panic`'s argument was `nil`;
  * the goroutine is not panicking;
  * `recover` was not called directly by a deferred function.

The `protect` function in the example below invokes the function argument `g` and protects callers from run-time panics raised by `g`.

```go
func protect(g func()) {
    defer func() {
        log.Println("done")  // Println executes normally even if there is a panic
        if x := recover(); x != nil {
            log.Printf("run time panic: %v", x)
        }
    }()
    log.Println("start")
    g()
}
```
