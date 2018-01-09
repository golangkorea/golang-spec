# Short variable declarations

A short variable declaration uses the syntax:

<pre>
<a id="ShortVarDecl">ShortVarDecl</a> = <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ":=" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> .
</pre>

It is shorthand for a regular [variable declaration](/Declarations%20and%20scope/variable_declarations.html) with initializer expressions but no types:

```go
"var" IdentifierList = ExpressionList .
```

```go
i, j := 0, 10
f := func() int { return 7 }
ch := make(chan int)
r, w := os.Pipe(fd)  // os.Pipe() returns two values
_, y, _ := coord(p)  // coord() returns three values; only interested in y coordinate
```

Unlike regular variable declarations, a short variable declaration may redeclare variables provided they were originally declared earlier in the same block (or the parameter lists if the block is the function body) with the same type, and at least one of the non-[blank](/Declarations%20and%20scope/blank_identifier.html) variables is new. As a consequence, redeclaration can only appear in a multi-variable short declaration. Redeclaration does not introduce a new variable; it just assigns a new value to the original.

```go
field1, offset := nextField(str, 0)
field2, offset := nextField(str, offset)  // redeclares offset
a, a := 1, 2                              // illegal: double declaration of a or no new variable if a was declared elsewhere
```

Short variable declarations may appear only inside functions. In some contexts such as the initializers for "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", or "[switch](/Statements/switch_statements.html)" statements, they can be used to declare local temporary variables.