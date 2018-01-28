# [패닉 처리](#handling-panics)

두 내장 함수인 `panic`과 `recover`는 [런타임 패닉](/Run-time panics/)과 프로그램에서 정의된  오류 조건들의 제어와 보고를 돕는다.

```go
func panic(interface{})
func recover() interface{}
```

함수 `F`를 실행하는 동안에, 명시적인 `panic` 호출이나 [런타임 패닉](/Run-time%20panics/)은 `F`의 실행을 중단시킨다. 그 뒤에 `F`가 [지연](/Statements/defer_statements.html)시킨 모든 함수들은 평상시와 같이 실행된다. 그 다음, `F`의 호출자가 수행하는 모든 지연된 함수들이 실행되고, 이런 식으로 이어져서 실행 중인 고루틴의 최상위 함수에 의해 지연된 모든 함수들이 실행된다. 그 시점에서, 프로그램이 종료되면서 `panic`에 인자로 주어진 값을 포함하는 오류 상태가 보고된다. 이러한 종료 절차를 *패닉킹*이라고 부른다.

```go
panic(42)
panic("unreachable")
panic(Error("cannot parse"))
```

`recover` 함수는 프로그램이 패닉킹 상태의 고루틴의 동작을 관리할 수 있도록 한다. 함수 `G`가 `recover`를 호출하는 함수 `D`를 호출하고 `G`가 실행되는 중에 동일한 고루틴의 함수에서 패닉이 발생한다고 가정해보자. 지연된 함수의 실행이 `D`에 도달했을 때, `D`의 `recover` 호출의 반환 값은 `panic`의 호출에 넘겨진 값이 될 것이다. `D`가 새로운 `panic`을 시작하지 않고 정상적으로 반환한다면, 패닉킹 절차는 중단된다. 이러한 경우, `G`와 `panic` 사이에 호출된 함수들의 상태는 버려질 것이고, 정상적인 실행이 재개된다. 이후 `D` 이전에 `G`가 지연시킨 모든 함수들이 실행되고,  `G`의 실행은 호출자에게 반환됨으로써 종료된다.

다음 조건들 중의 하나라도 해당하는 경우, `recover`의 반환값은 `nil`이다.

  * `panic`의 인자가 `nil`인 경우;
  * 고루틴이 패닉킹에 빠지지 않은 경우;
  * 지연된 함수에서 `recover`를 직접적으로 호출하지 않은 경우.

아래의 예제에 있는 `protect` 함수는 함수 인자 `g`를 호출하고 `g`에 의해 발생되는 런타임 패닉들로부터 호출자를 보호한다.

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
