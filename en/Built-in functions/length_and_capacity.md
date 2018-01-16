# [Length and capacity](#length-and-capacity)

The built-in functions len and cap take arguments of various types and return a result of type int. The implementation guarantees that the result always fits into an int.

```go
Call      Argument type    Result

len(s)    string type      string length in bytes
          [n]T, *[n]T      array length (== n)
          []T              slice length
          map[K]T          map length (number of defined keys)
          chan T           number of elements queued in channel buffer

cap(s)    [n]T, *[n]T      array length (== n)
          []T              slice capacity
          chan T           channel buffer capacity
```

The capacity of a slice is the number of elements for which there is space allocated in the underlying array. At any time the following relationship holds:

```go
0 <= len(s) <= cap(s)
```

The length of a nil slice, map or channel is 0. The capacity of a nil slice or channel is 0.

The expression `len(s)` is [constant](/Constants/) if s is a string constant. The expressions `len(s)` and `cap(s)` are constants if the type of s is an array or pointer to an array and the expression s does not contain [channel receives](/Expressions/receive_operator.html) or (non-constant) [function calls](/Expressions/calls.html); in this case s is not evaluated. Otherwise, invocations of len and cap are not constant and s is evaluated.

```go
const (
	c1 = imag(2i)                    // imag(2i) = 2.0 is a constant
	c2 = len([10]float64{2})         // [10]float64{2} contains no function calls
	c3 = len([10]float64{c1})        // [10]float64{c1} contains no function calls
	c4 = len([10]float64{imag(2i)})  // imag(2i) is a constant and no function call is issued
	c5 = len([10]float64{imag(z)})   // invalid: imag(z) is a (non-constant) function call
)
var z complex128
```