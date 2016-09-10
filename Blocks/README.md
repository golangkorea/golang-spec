# Blocks

A *block* is a possibly empty sequence of declarations and statements within matching brace brackets.

<pre>
<a id="Block">Block</a> = "{" <a href="#StatementList">StatementList</a> "}" .
<a id="StatementList">StatementList</a> = { <a href="/Statements/#Statement">Statement</a> ";" } .
</pre>

In addition to explicit blocks in the source code, there are implicit blocks:

The universe block encompasses all Go source text.
Each package has a package block containing all Go source text for that package.
Each file has a file block containing all Go source text in that file.
Each "if", "for", and "switch" statement is considered to be in its own implicit block.
Each clause in a "switch" or "select" statement acts as an implicit block.
Blocks nest and influence scoping.