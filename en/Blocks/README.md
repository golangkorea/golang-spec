# [Blocks](#blocks)

A *block* is a possibly empty sequence of declarations and statements within matching brace brackets.

<pre>
<a id="Block">Block</a> = "{" <a href="#StatementList">StatementList</a> "}" .
<a id="StatementList">StatementList</a> = { <a href="/Statements/#Statement">Statement</a> ";" } .
</pre>

In addition to explicit blocks in the source code, there are implicit blocks:

  1. The *universe block* encompasses all Go source text.
  2. Each [package](/Packages/) has a *package block* containing all Go source text for that package.
  3. Each file has a *file block* containing all Go source text in that file.
  4. Each "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", and "[switch](/Statements/switch_statements.html)" statement is considered to be in its own implicit block.
  5. Each clause in a "[switch](/Statements/switch_statements.html)" or "[select](/Statements/select_statements.html)" statement acts as an implicit block.

Blocks nest and influence scoping.
