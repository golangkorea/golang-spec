# [패닉 처리](#handling-panics)

내장 함수 `panic`과 `recover`는 [런타임 패닉](/Run-time%20panics/)과 프로그램에서 정의한 오류 조건들을 처리하고 보고하는 역할을 담당한다.

```go
func panic(interface{})
func recover() interface{}
```

함수 `F`가 실행되고 있을 때, 명시적인 `panic` 을 명시적으로 호출하거나 [런타임 패닉](/Run-time%20panics/)이 발생하면 `F`의 실행은 종료된다. 그런 다음, `F` 함수 안에서 [defer 예약어를 통해 지연된](/Statements/defer_statements.html)모든 함수들이 평상시처럼 실행된다. 다음으로 `F` 함수를 호출한 곳에 있는 모든 지연된 함수들이 실행되고, 이런 식으로 이어져서 실행 중인 고루틴의 최상위 함수에 의해 지연된 모든 함수들까지 실행된다. 그 시점에서, 프로그램이 종료되면서 `panic`에 인자로 주어진 값이 포함된 오류 상태가 보고된다. 이러한 종료 절차를 *패닉킹(panicking)*이라고 부른다.

```go
panic(42)
panic("unreachable")
panic(Error("cannot parse"))
```

프로그램은 `recover` 함수를 통해 패닉킹 고루틴의 동작을 관리할 수 있다. 함수 `G`가 `recover`를 호출하는 함수 `D`를 지연하고 `G`가 실행되는 같은 고루틴의 함수에서 패닉이 발생했다고 가정해보자. 지연된 함수의 실행이 `D`에 도달했을 때,  `panic` 호출시 인자로 전달된 값이 `D`가 호출한 `recover` 의 반환 값이 될 것이다. `D`가 새로운 `panic`을 시작하지 않고 정상적으로 반환된다면, 패닉킹 절차는 중단된다. 이러한 경우, `G`와 `panic`  호출 사이에 호출된 함수들의 상태는 버려질 것이고, 정상적인 실행이 재개된다. 이후 `D` 이전에 `G`가 지연시킨 모든 함수들이 실행되고,  `G`의 실행은 호출자에게 반환됨으로써 종료된다.

다음 조건들 중의 하나라도 해당하는 경우, `recover`의 반환값은 `nil`이다.

  * `panic`의 인자가 `nil`인 경우;
  * 고루틴이 패닉킹이 아닌 경우;
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
