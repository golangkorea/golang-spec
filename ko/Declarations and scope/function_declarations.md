# Function declarations

A function declaration binds an identifier, the function name, to a function.

<pre>
<a id="FunctionDecl">FunctionDecl</a> = "func" <a href="#FunctionName">FunctionName</a> ( <a href="#Function">Function</a> | <a href="/Types/function_types.html#Signature">Signature</a> ) .
<a id="FunctionName">FunctionName</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
<a id="Function">Function</a>     = <a href="/Types/function_types.html#Signature">Signature</a> <a href="#FunctionBody">FunctionBody</a> .
<a id="FunctionBody">FunctionBody</a> = <a href="/Blocks/#Block">Block</a> .
</pre>

If the function's [signature](/Types/function_types.html) declares result parameters, the function body's statement list must end in a [terminating statement](/Statements/terminating_statements.html).

```go
func IndexRune(s string, r rune) int {
    for i, c := range s {
        if c == r {
            return i
        }
    }
    // invalid: missing return statement
}
```

A function declaration may omit the body. Such a declaration provides the signature for a function implemented outside Go, such as an assembly routine.

```go
func min(x int, y int) int {
    if x < y {
        return x
    }
    return y
}

func flushICache(begin, end uintptr)  // implemented externally
```