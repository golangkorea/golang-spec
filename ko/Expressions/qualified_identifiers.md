# Qualified identifiers

A qualified identifier is an identifier qualified with a package name prefix. Both the package name and the identifier must not be [blank](/Declarations%20and%20scope/blank_identifier.html).

<pre>
<a id="QualifiedIdent">QualifiedIdent</a> = <a href="/Packages/package_clause.html#PackageName">PackageName</a> "." <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
</pre>

A qualified identifier accesses an identifier in a different package, which must be [imported](/Packages/import_declarations.html). The identifier must be [exported](/Declarations%20and%20scope/exported_identifiers.html) and declared in the [package block](/Blocks/) of that package.

```go
math.Sin    // denotes the Sin function in package math
```
