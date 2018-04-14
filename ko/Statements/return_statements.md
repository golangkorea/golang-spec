# [return 문](#return-statements)

함수 `F` 내에서 "return" 문은 `F`의 실행을 종료하고, 한개 이상의 반환 값을 제공할 수 있다. `F`에 의해 실행이 [지연되었던](/Statements/defer_statements.html) 함수는 `F`가 호출자에게 반환되기 전에 실행된다.

<pre>
<a id="ReturnStmt">ReturnStmt</a> = "return" [ <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> ] .
</pre>

반환값이 없는 함수내에서는, "return" 문은 반환 값을 명시하면 안된다.

```go
func noResult() {
    return
}
```

반환 타입을 가지고 있는 함수로 부터 값을 반환하는 3가지 방법이 있다.

  1. 반환 값 또는 복수의 값은 "return" 문에 명시적으로 나열될 수 있다. 각 식은 단일-값이어야 하고 함수의 반환 타입의 해당 요소에 [할당가능](/Properties%20of%20types%20and%20values/assignability.html)해야 한다.

```go
func simpleF() int {
    return 2
}

func complexF1() (re float64, im float64) {
    return -7.0, -4.0
}
```

  2. "return" 문내 식 목록은 다중-값 함수에 대한 호출일 수도 있다. 그 효과는 마치 함수로 부터 반환된 각 값들이 해당 값의 타입을 가지는 임시 변수에 할당되고, "return" 문이 이 변수들을 나열하면서 이전 경우의 규칙들이 적용되는 것이다.

```go
func complexF2() (re float64, im float64) {
    return complexF1()
}
```

  3. 함수의 반환 타입이 [반환 매개변수들](/Types/function_types.html)의 이름을 명시하는 경우는 식 목록을 생략할 수도 있다. 반환 매개변수들은 보통의 로컬 변수들처럼 동작하고 함수는 필요에 따라 값을 할당할 수 있다. "return" 문은 이 변수들의 값을 반환한다.

```go
func complexF3() (re float64, im float64) {
    re = 7.0
    im = 4.0
    return
}

func (devnull) Write(p []byte) (n int, _ error) {
    n = len(p)
    return
}
```

어떤 식으로 선언되던, 모든 반환 값들은 함수에 진입하는 시점에 해당 타입의 [제로 값들](/Program%20initialization%20and%20execution/the_zero_value.html)로 초기화 된다. 반환 값을 명시하는 "return" 문은 실행이 지연된 함수가 실행되기 전에 반환 매개변수에 값을 설정한다.

구현시 제한 사항: 반환 위치의 [범위](/Declarations%20and%20scope/) 안에 결과 매개 변수로 같은 이름을 가진 다른 개체 (상수, 타입, 변수)가 사용된다면  컴파일러는 "return" 문 내에 비어있는 식 목록을 허용하지 않을 수도 있다.

```go
func f(n int) (res int, err error) {
    if _, err := f(n-1); err != nil {
        return  // 유효하지 않은 return 문: err 가 쉐도우되었다.
    }
    return
}
```
