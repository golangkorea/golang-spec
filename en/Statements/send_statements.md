# [Send statements](#send-statements)

A send statement sends a value on a channel. The channel expression must be of [channel type](/Types/channel_types.html), the channel direction must permit send operations, and the type of the value to be sent must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to the channel's element type.

<pre>
<a id="SendStmt">SendStmt</a> = <a href="#Channel">Channel</a> "&lt;-" <a href="/Expressions/operators.html#Expression">Expression</a> .
<a id="Channel">Channel</a>  = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

Both the channel and the value expression are evaluated before communication begins. Communication blocks until the send can proceed. A send on an unbuffered channel can proceed if a receiver is ready. A send on a buffered channel can proceed if there is room in the buffer. A send on a closed channel proceeds by causing a [run-time panic](/Run-time%20panics/). A send on a `nil` channel blocks forever.

```go
ch <- 3  // send value 3 to channel ch
```
