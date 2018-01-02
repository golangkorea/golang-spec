# [채널 타입](#channel-types)

채널은 [동시에 실행중인 함수들](/Statements/go_statements.html)이 명시된 요소 타입의 값들을 [주고]((/Statements/send_statements.html)) [받으며](/Expressions/receive_operator.html) 통신할 수 있는 매커니즘을 제공한다. 초기화 되지 않은 채널의 값은 `nil`이다.

<pre>
<a id="ChannelType">ChannelType</a> = ( "chan" | "chan" "<-" | "<-" "chan" ) <a href="/Types/array_types.html#ElementType">ElementType</a> .
</pre>

채널에 추가로 붙이는 `<-` 연산자는 *송신*과 *수신*의 *방향*을 나타낸다. 방향이 주어지지 않은 경우, 채널은 *양방향*이다. [타입변환](/Expressions/conversions.html) 혹은 [할당](/Statements/assignments.html)을 통해서 채널은 송신과 수신중 한 방향으로 제한될 수 있다.

```
chan T          // 타입 T의 값을 보낼 수도 있고 받을 수도 있다.
chan<- float64  // float64 값들만 보낼 수 있다.
<-chan int      // int 값들만 받을 수 있다.
```

`<-` 연산자는 최대한 가장 왼쪽 채널과 연계된다:

```
chan<- chan int    // chan<- (chan int) 과 같다
chan<- <-chan int  // chan<- (<-chan int) 과 같다
<-chan <-chan int  // <-chan (<-chan int) 과 같다
chan (<-chan int)
```

새로 초기화 된 채널값은 내장 함수인 [`make`](/Built-in%20functions/making_slices,_maps_and_channels.html)에 채널 타입과 추가로 *용량*을 인자로 전달해서 만들어 진다.

```
make(chan int, 100)
```

요소의 수를 나타내는 용량은 채널안에 있는 버퍼의 크기를 정한다. 용량이 0이던지 전혀 주어지지 않았다면, 채널에 버퍼가 없는 것이며 이 경우 통신은 송신자와 수신자 모두가 준비된 상태에서만 성공한다. 반면에, 버퍼가 있다면 (송신때) 버퍼가 완전히 채워진 경우와 (수신때) 완전히 비어있는 경우를 제외하고 통신은 블로킹없이 성공한다. `nil` 채널은 통신할 수 없다.

채널은 내장함수 [`close`](/Built-in%20functions/close.html)를 사용해서 닫을 수 있다. [수신 연산자](/Expressions/receive_operator.html)가 여러 값을 할당하는 형식을 통해 수신된 값이 채널이 닫히기 전에 보내진 것인지의 여부를 확인 할 수 있다. 

[송신 구문](/Statements/send_statements.html), [수신 연산](/Expressions/receive_operator.html), 그리고 내장 함수인 [`cap`](/Built-in%20functions/length_and_capacity.html) 과 [`len`](/Built-in%20functions/length_and_capacity.html)의 호출시 특별한 동기화 없이도 여러 고루틴에서 하나의 채널을 공유할 수 있다. 채널들은 선입-선출 큐(first-in-first-out queues)처럼 동작한다. 예를 들어, 한 고루틴에서 어떤 채널에 값들을 송신하고 다른 고루틴에서 수신하면, 값들은 송신한 순서대로 수신된다.