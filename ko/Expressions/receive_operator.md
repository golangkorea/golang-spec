# Receive operator

For an operand ch of [channel type](/Types/channel_types.html), the value of the receive operation <-ch is the value received from channel ch. direction must permit receive operations, and type of operation element channel. expression blocks until a available. receiving nil forever. on <a href =/Built-in%20functions/close.html>closed</a> channel can always proceed immediately, yielding the element type's [zero value](/Program%20initialization%20and%20execution/the_zero_value.html) after any previously sent values have been received.

    v1 := <-ch
    v2 = <-ch
    f(<-ch)
    <-strobe  // wait until clock pulse and discard received value
    

A receive expression used in an [assignment](/Statements/assignments.html) or initialization of the special form

    x, ok = <-ch
    x, ok := <-ch
    var x, ok = <-ch
    

yields an additional untyped boolean result reporting whether the communication succeeded. The value of ok is true if the value received was delivered by a successful send operation to the channel, or false if it is a zero value generated because the channel is closed and empty.