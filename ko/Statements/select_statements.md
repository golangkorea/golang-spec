# Select statements

A "select" statement chooses which of a set of possible [send](/Statements/send_statements.html) or [receive](/Expressions/receive_operator.html) operations will proceed. It looks similar to a "[switch](/Statements/switch_statements.html)" statement but with the cases all referring to communication operations.

<pre>
<a id="SelectStmt">SelectStmt</a> = "select" "{" { <a href="#CommClause">CommClause</a> } "}" .
<a id="CommClause">CommClause</a> = <a href="#CommCase">CommCase</a> ":" <a href="/Blocks/#StatementList">StatementList</a> .
<a id="CommCase">CommCase</a>   = "case" ( <a href="/Statements/send_statements.html#SendStmt">SendStmt</a> | <a href="#RecvStmt">RecvStmt</a> ) | "default" .
<a id="RecvStmt">RecvStmt</a>   = [ <a href="/Blocks/#ExpressionList">ExpressionList</a> "=" | <a href="/Blocks/#IdentifierList">IdentifierList</a> ":=" ] <a href="#RecvExpr">RecvExpr</a> .
<a id="RecvExpr">RecvExpr</a>   = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

A case with a RecvStmt may assign the result of a RecvExpr to one or two variables, which may be declared using a [short variable declaration](/Declarations%20and%20scope/short_variable_declarations.html). The RecvExpr must be a (possibly parenthesized) receive operation. There can be at most one default case and it may appear anywhere in the list of cases.

Execution of a "select" statement proceeds in several steps:

  1. For all the cases in the statement, the channel operands of receive operations and the channel and right-hand-side expressions of send statements are evaluated exactly once, in source order, upon entering the "select" statement. The result is a set of channels to receive from or send to, and the corresponding values to send. Any side effects in that evaluation will occur irrespective of which (if any) communication operation is selected to proceed. Expressions on the left-hand side of a RecvStmt with a short variable declaration or assignment are not yet evaluated.
  2. If one or more of the communications can proceed, a single one that can proceed is chosen via a uniform pseudo-random selection. Otherwise, if there is a default case, that case is chosen. If there is no default case, the "select" statement blocks until at least one of the communications can proceed.
  3. Unless the selected case is the default case, the respective communication operation is executed.
  4. If the selected case is a RecvStmt with a short variable declaration or an assignment, the left-hand side expressions are evaluated and the received value (or values) are assigned.
  5. The statement list of the selected case is executed.

Since communication on nil channels can never proceed, a select with only nil channels and no default case blocks forever.

```go
var a []int
var c, c1, c2, c3, c4 chan int
var i1, i2 int
select {
case i1 = <-c1:
    print("received ", i1, " from c1\n")
case c2 <- i2:
    print("sent ", i2, " to c2\n")
case i3, ok := (<-c3):  // same as: i3, ok := <-c3
    if ok {
        print("received ", i3, " from c3\n")
    } else {
        print("c3 is closed\n")
    }
case a[f()] = <-c4:
    // same as:
    // case t := <-c4
    //  a[f()] = t
default:
    print("no communication\n")
}

for {  // send random sequence of bits to c
    select {
    case c <- 0:  // note: no statement, no fallthrough, no folding of cases
    case c <- 1:
    }
}

select {}  // block forever
```