# Expression statements

With the exception of specific built-in functions, function and method [calls](/Expressions/calls.html) and [receive operations](/Expressions/receive_operator.html) can appear in statement context. Such statements may be parenthesized.

<pre>
<a id="ExpressionStmt">ExpressionStmt</a> = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

The following built-in functions are not permitted in statement context:

    append cap complex imag len make new real
    unsafe.Alignof unsafe.Offsetof unsafe.Sizeof
    

    h(x+y)
    f.Close()
    <-ch
    (<-ch)
    len("foo")  // illegal if len is the built-in function