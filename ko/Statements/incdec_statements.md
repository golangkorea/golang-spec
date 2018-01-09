# IncDec statements

The "++" and "--" statements increment or decrement their operands by the untyped [constant](/Constants/) 1. As with an assignment, the operand must be [addressable](/Expressions/address_operators.html) or a map index expression.

<pre>
<a id="IncDecStmt">IncDecStmt</a> = <a href="/Expressions/operators.html#Expression">Expression</a> ( "++" | "--" ) .
</pre>

The following [assignment statements](/Statements/assignments.html) are semantically equivalent:

    IncDec statement    Assignment
    x++                 x += 1
    x--                 x -= 1