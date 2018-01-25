# [수신 연산자](#receive-operators)

[채널 타입](/Types/channel_types.html)의 피연산자 `ch`에 대해, 수신 연산 `<-ch`의 값은 채널 `ch`로 부터 수신한 값이다. 채널의 방향은 수신 연산을 허용해야 하며 수신 연산의 타입은 채널의 요소 타입이다. 이와 같은 표현식은 값이 수신 가능할 때까지 실행을 차단한다. `nil` 채널에서 수신할 때는 실행이 영구히 차단된다. [이미 닫혀진](/Built-in%20functions/close.html) 채널에서 수신할 때는 즉각 실행되며 그 전에 보내진 값들이 수신되고 난 이후에는 요소 타입의 [제로값](/Program%20initialization%20and%20execution/the_zero_value.html)을 생산한다

```go
v1 := <-ch
v2 = <-ch
f(<-ch)
<-strobe  // 다음 클럭 펄스가 일어날때 까지 기다리고 난 후 수신한 값을 버린다.
```

다음과 같이 [할당 구문](/Statements/assignments.html)에 사용된 수신 표현이나 특수 형태의 초기화는

```go
x, ok = <-ch
x, ok := <-ch
var x, ok = <-ch
```

추가로 수신의 성공 여부를 알려주는 미지정 타입 불리언 값을 생산한다. 채널에 성공적으로 송신이 되어 값을 수신한 경우 `ok`의 값이 `true`이고, 채널이 닫혔거나 비어 있어 제로값이 생성된 경우는 `false`이다.
