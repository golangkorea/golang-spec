# [Array types](#array-types)

An array is a numbered sequence of elements of a single type, called the element type. The number of elements is called the length and is never negative.

<pre>
<a id="ArrayType">ArrayType</a>   = "[" <a href="#ArrayLength">ArrayLength</a> "]" <a href="#ElementType">ElementType</a> .
<a id="ArrayLength">ArrayLength</a> = [Expression](/Expressions/) .
<a id="ElementType">ElementType</a> = [Type](/Types/) .
</pre>

The length is part of the array's type; it must evaluate to a non-negative [constant](/Constants/) representable by a value of type `int`. The length of array a can be discovered using the built-in function [len](/Built-in%20functions/length_and_capacity.html). The elements can be addressed by integer [indices](/Expressions/index_expressions.html) 0 through `len(a)-1`. Array types are always one-dimensional but may be composed to form multi-dimensional types.

```go
[32]byte
[2*N] struct { x, y int32 }
[1000]*float64
[3][5]int
[2][2][2]float64  // same as [2]([2]([2]float64))
```