# [평가의 순서](#order-of-evaluation)

패키지 레벨에서, [변수 선언문들](/Declarations%20and%20scope/variable_declarations.html)에 있는 개별 초기화 식의 평가 순서는 [초기화 종속성](/Program%20initialization%20and%20execution/package_initialization.html)이 결정한다. 그렇지 않은 경우, 식의 [피연산자](/Expressions/operands.html)를 평가할 때나 할당문, 혹은 [반환문](/Statements/return_statements.html), 모든 함수 호출, 메서드 호출, 그리고 통신 연산들은 어휘적으로 왼쪽에서 오른쪽으로 순차적으로 평가된다.



예를 들어, (함수-로컬) 할당문에서

```go
y[f()], ok = g(h(), i()+x[j()], <-c), k()
```

함수 호출과 통신은 `f()`, `h()`, `i()`, `j()`, `<-c`, `g()`, 그리고 `k()`의 순서로 일어 난다. 그러나, 이러한 이벤트들이 `x`의 평가및 인덱싱 그리고 `y`의 평가와 비교해서 어떤 순서로 일어 날지는 지정되지 않는다.

```go
a := 1
f := func() int { a++; return a }
x := []int{a, f()}            // x는 [1, 2]이거나 [2, 2]일 수도 있다: a와 f()의 평가 순서는 지정되지 않는다.
m := map[int]int{a: 1, a: 2}  // m은 {2: 1}이거나 {2: 2}일 수도 있다: 두 맵 할당의 평가 순서를 지정되지 않는다
n := map[int]int{a: f()}      // n은 {2: 3}이거나 {3: 3}일 수도 있다: 키와 값의 평가 순서는 지정되지 않는다.
```

패키지 레벨에서, 초기화 종속성이 개별 초기화 식에 대한 왼쪽에서-오른쪽 규칙를 무시하시만, 개별 식내의 피연산자에 대해서는 무시하지 않는다.

```go
var a, b, c = f() + v(), g(), sqr(u()) + v()

func f() int        { return c }
func g() int        { return a }
func sqr(x int) int { return x*x }

// 함수 u와 v는 다른 모든 변수와 함수에 의존하지 않는다
```

함수 호출은 `u()`, `sqr()`, `v()`, `f()`, `v()`, 그리고 `g()`의 순서로 일어난다.

단일 식에서 부동 소수점 연산은 연산자의 결합(associativity)에 따라 평가된다. 괄호는 명시적으로 함으로써 원래의 결합을 무시하고 평가할 수도 있다. `x + (y + z)`식을 보면 `x`를 더하기 전에 `y + z`가 더해졌다.
