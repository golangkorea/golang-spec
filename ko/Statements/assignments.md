# Assignments

<pre>
<a id="Assignment">Assignment</a> = <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> <a href="#assign_op">assign_op</a> <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> .
&nbsp;
<a id="assign_op">assign_op</a> = [ <a href="/Expressions/operators.html#add_op">add_op</a> | <a href="/Expressions/operators.html#mul_op">mul_op</a> ] "=" .
</pre>

Each left-hand side operand must be [addressable](/Expressions/address_operators.html), a map index expression, or (for = assignments only) the [blank identifier](/Declarations%20and%20scope/blank_identifier.html). Operands may be parenthesized.

```go
x = 1
*p = f()
a[i] = 23
(k) = <-ch  // same as: k = <-ch
```

An assignment operation x op= y where op is a binary [arithmetic operation](/Expressions/arithmetic_operators.html) is equivalent to x = x op (y) but evaluates x only once. The op= construct is a single token. In assignment operations, both the left- and right-hand expression lists must contain exactly one single-valued expression, and the left-hand expression must not be the blank identifier.

```go
a[i] <<= 2
i &^= 1<<n
```

A tuple assignment assigns the individual elements of a multi-valued operation to a list of variables. There are two forms. In the first, the right hand operand is a single multi-valued expression such as a function call, a [channel](/Types/channel_types.html) or [map](/Types/map_types.html) operation, or a [type assertion](/Expressions/type_assertions.html). The number of operands on the left hand side must match the number of values. For instance, if f is a function returning two values,

```go
x, y = f()
```

assigns the first value to x and the second to y. In the second form, the number of operands on the left must equal the number of expressions on the right, each of which must be single-valued, and the nth expression on the right is assigned to the nth operand on the left:

```go
one, two, three = '一', '二', '三'
```

The [blank identifier](/Declarations%20and%20scope/blank_identifier.html) provides a way to ignore right-hand side values in an assignment:

```go
_ = x       // evaluate x but ignore it
x, _ = f()  // evaluate f() but ignore second result value
```

The assignment proceeds in two phases. First, the operands of [index expressions](/Expressions/index_expressions.html) and [pointer indirections](/Expressions/address_operators.html) (including implicit pointer indirections in [selectors](/Expressions/selectors.html)) on the left and the expressions on the right are all [evaluated in the usual order](/Expressions/order_of_evaluation.html). Second, the assignments are carried out in left-to-right order.

```go
a, b = b, a  // exchange a and b

x := []int{1, 2, 3}
i := 0
i, x[i] = 1, 2  // set i = 1, x[0] = 2

i = 0
x[i], i = 2, 1  // set x[0] = 2, i = 1

x[0], x[0] = 1, 2  // set x[0] = 1, then x[0] = 2 (so x[0] == 2 at end)

x[1], x[3] = 4, 5  // set x[1] = 4, then panic setting x[3] = 5.

type Point struct { x, y int }
var p *Point
x[2], p.x = 6, 7  // set x[2] = 6, then panic setting p.x = 7

i = 2
x = []int{3, 5, 7}
for i, x[i] = range x {  // set i, x[2] = 0, x[0]
    break
}
// after this loop, i == 0 and x == []int{3, 5, 3}
```

In assignments, each value must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to the type of the operand to which it is assigned, with the following special cases:

  1. Any typed value may be assigned to the blank identifier.
  2. If an untyped constant is assigned to a variable of interface type or the blank identifier, the constant is first [converted](/Expressions/conversions.html) to its [default type](/Constants/).
  3. If an untyped boolean value is assigned to a variable of interface type or the blank identifier, it is first converted to type `bool`.