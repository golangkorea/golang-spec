# Constant declarations

A constant declaration binds a list of identifiers (the names of the constants) to the values of a list of [constant expressions](/Expressions/constant_expressions.html). The number of identifiers must be equal to the number of expressions, and the nth identifier on the left is bound to the value of the nth expression on the right.

<pre>
<a id="ConstDecl">ConstDecl</a>      = "const" ( <a href="#ConstSpec">ConstSpec</a> | "(" { <a href="#ConstSpec">ConstSpec</a> ";" } ")" ) .
<a id="ConstSpec">ConstSpec</a>      = <a href="#IdentifierList">IdentifierList</a> [ [ <a href="/Types/#Type">Type</a> ] "=" <a href="#ExpressionList">ExpressionList</a> ] .

<a id="IdentifierList">IdentifierList</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> { "," <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> } .
<a id="ExpressionList">ExpressionList</a> = <a href="/Expressions/operators.html#Expression">Expression</a> { "," <a href="/Expressions/operators.html#Expression">Expression</a> } .
</pre>

If the type is present, all constants take the type specified, and the expressions must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to that type. If the type is omitted, the constants take the individual types of the corresponding expressions. If the expression values are untyped [constants](/Constants/), the declared constants remain untyped and the constant identifiers denote the constant values. For instance, if the expression is a floating-point literal, the constant identifier denotes a floating-point constant, even if the literal's fractional part is zero.

    const Pi float64 = 3.14159265358979323846
    const zero = 0.0         // untyped floating-point constant
    const (
        size int64 = 1024
        eof        = -1  // untyped integer constant
    )
    const a, b, c = 3, 4, "foo"  // a = 3, b = 4, c = "foo", untyped integer and string constants
    const u, v float32 = 0, 3    // u = 0.0, v = 3.0
    

Within a parenthesized const declaration list the expression list may be omitted from any but the first declaration. Such an empty list is equivalent to the textual substitution of the first preceding non-empty expression list and its type if any. Omitting the list of expressions is therefore equivalent to repeating the previous list. The number of identifiers must be equal to the number of expressions in the previous list. Together with the [iota constant generator](/Declarations%20and%20scope/iota.html) this mechanism permits light-weight declaration of sequential values:

    const (
        Sunday = iota
        Monday
        Tuesday
        Wednesday
        Thursday
        Friday
        Partyday
        numberOfDays  // this constant is not exported
    )