# [send 문](#send-statements)

send 문은 채널에 값을 보낸다. 채널 식은 [채널 타입](/Types/channel_types.html)이어야 하고, 채널 방향은 송신 연산을 허용하는 것이어야 하며, 송신하는 값의 타입은 채널의 요소 타입에 [할당할 수 있는](/Properties%20of%20types%20and%20values/assignability.html) 것이어야 한다.

<pre>
<a id="SendStmt">SendStmt</a> = <a href="#Channel">Channel</a> "&lt;-" <a href="/Expressions/operators.html#Expression">Expression</a> .
<a id="Channel">Channel</a>  = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

채널과 값에 대한 식은 통신을 시작하기 전에 평가된다. 송신할 수 있는 상태가 될 때까지 통신은 차단된다. 버퍼가 없는 채널은 수신자가 준비되었을 때 송신이 가능하다. 버퍼가 있는 채널은 버퍼에 여유공간이 있을때 송신이 가능하다. 닫힌 채널에 송신하면 [런타입 패닉](/Run-time%20panics/)이 발생한다. `nil` 채널에 송신은 영원히 차단된다.

```go
ch <- 3  // 채널 ch로 값 3을 송신한다.
```
