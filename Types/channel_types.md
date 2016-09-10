# Channel types

A channel provides a mechanism for [concurrently executing functions](/Statements/go_statements.html) to communicate by [sending](/Statements/send_statements.html) and [receiving](/Expressions/receive_operator.html) values of a specified element type. The value of an uninitialized channel is `nil`.

<pre>
<a id="ChannelType">ChannelType</a> = ( "chan" | "chan" "<-" | "<-" "chan" ) <a href="/Types/array_types.html#ElementType">ElementType</a> .
</pre>

The optional <- operator specifies the channel *direction*, *send* or *receive*. If no direction is given, the channel is *bidirectional*. A channel may be constrained only to send or only to receive by [conversion](/Expressions/conversions.html) or [assignment](/Statements/assignments.html).

```
chan T          // can be used to send and receive values of type T
chan<- float64  // can only be used to send float64s
<-chan int      // can only be used to receive ints
```

The <- operator associates with the leftmost chan possible:

```
chan<- chan int    // same as chan<- (chan int)
chan<- <-chan int  // same as chan<- (<-chan int)
<-chan <-chan int  // same as <-chan (<-chan int)
chan (<-chan int)
```

A new, initialized channel value can be made using the built-in function [make](/Built-in%20functions/making_slices,_maps_and_channels.html), which takes the channel type and an optional *capacity* as arguments:

```
make(chan int, 100)
```

The capacity, in number of elements, sets the size of the buffer in the channel. If the capacity is zero or absent, the channel is unbuffered and communication succeeds only when both a sender and receiver are ready. Otherwise, the channel is buffered and communication succeeds without blocking if the buffer is not full (sends) or not empty (receives). A `nil` channel is never ready for communication.

A channel may be closed with the built-in function [close](/Built-in%20functions/close.html). The multi-valued assignment form of the [receive operator](/Expressions/receive_operator.html) reports whether a received value was sent before the channel was closed.

A single channel may be used in [send statements](/Statements/send_statements.html), [receive operations](/Expressions/receive_operator.html), and calls to the built-in functions [cap](/Built-in%20functions/length_and_capacity.html) and [len](/Built-in%20functions/length_and_capacity.html) by any number of goroutines without further synchronization. Channels act as first-in-first-out queues. For example, if one goroutine sends values on a channel and a second goroutine receives them, the values are received in the order sent.

