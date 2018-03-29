# [send 문](#send-statements)

send 문은 채널에 한 값을 보낸다. 채널 식은 [채널 타입](/Types/channel_types.html)이어야 하고, 채널은 송신 연산을 허용하는 방향을 가져야 하며, 송신되는 값의 타입은 채널의 요소 타입에 [할당할 수 있는](/Properties%20of%20types%20and%20values/assignability.html) 타입이어야 한다.

<pre>
<a id="SendStmt">SendStmt</a> = <a href="#Channel">Channel</a> "&lt;-" <a href="/Expressions/operators.html#Expression">Expression</a> .
<a id="Channel">Channel</a>  = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

통신이 시작되기 전에 채널과 값의 식 모두가 평가된다. 통신은 송신이 진행될 수 있을 때까지 블록도니다. 버퍼가 없는 채널에는 수신자가 준비가 되었다면 송신이 진행될 수 있다. 버퍼가 있는 채널에는 버퍼에 여유공간이 있다면 송신이 진행될 수 있다. 닫힌 채널에 송신하면 [런타입 패닉](/Run-time%20panics/)이 유발된다. `nil` 채널에 송신하면 영원히 블록된다.

```go
ch <- 3  // 값 3을 채널 ch로 보낸다
```
