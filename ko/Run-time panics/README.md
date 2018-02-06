# [런타임 패닉](#run-time-panics)

배열의 범위를 넘어서 값을 접근하려는 시도와 같은 실행 에러는 내장 함수인 [panic](/Built-in%20functions/handling_panics.html)을 구현-정의형(implementation-defined) 인터페이스 타입 `runtime.Error`를 가지고 호출하는 것과 같은 *런타임 패닉*을 일으킨다. 그 타입은 미리 선언된 인터페이스 타입인 [error](/Errors/)를 만족시킨다. 런타임 에러의 독특한 조건을 표현하는 정확한 에러 값은 명시되지 않는다.

```go
package runtime

type Error interface {
    error
    // 어쩌면 다른 메서드들도 있을 수 있다.
}
```
