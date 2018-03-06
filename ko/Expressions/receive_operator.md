# [수신 연산자](#receive-operators)

[채널 타입](/Types/channel_types.html)의 피연산자 `ch`에 대해, 수신 연산 `<-ch`의 값은 채널 `ch`로 부터 수신한 값이다. 채널의 방향은 수신 연산을 허용해야 하며 수신 연산의 타입은 채널의 요소 타입이다. 값이 수신 가능할 때까지 식은 실행되지 않는다. `nil` 채널에서 수신할 때는 영원히 실행되지 않는다. [이미 닫혀진](/Built-in%20functions/close.html) 채널에 대한 수신 연산은 바로 처리할 수 있으며, 그 전에 보내진 값들이 수신되고 난 이후의 수신 연산 결과는 요소 타입의 [제로값](/Program%20initialization%20and%20execution/the_zero_value.html)이 된다.

```go
v1 := <-ch
v2 = <-ch
f(<-ch)
<-strobe  // 다음 클럭 펄스가 일어날때 까지 기다리고 난 후 수신한 값을 버린다.
```

[할당](/Statements/assignments.html)이나 특수 형태의 초기화에 사용된 수신 식(expression)은

```go
x, ok = <-ch
x, ok := <-ch
var x, ok = <-ch
```

통신의 성공 여부를 알려주는 미지정 타입의 불리언 값을 추가적으로 제공한다. 성공적으로 채널에 송신되어 값을 수신한 경우 `ok` 값은 `true`이고, 채널이 닫혔거나 비어있어서 제로 값이 생성된 경우 `ok` 값은 `false`다.
