# Import declarations

An import declaration states that the source file containing the declaration depends on functionality of the *imported* package ([§Program initialization and execution](/Program%20initialization%20and%20execution/)) and enables access to [exported](/Declarations%20and%20scope/exported_identifiers.html) identifiers of that package. The import names an identifier (PackageName) to be used for access and an ImportPath that specifies the package to be imported.

<pre>
<a id="ImportDecl">ImportDecl</a>       = "import" ( <a href="#ImportSpec">ImportSpec</a> | "(" { <a href="#ImportSpec">ImportSpec</a> ";" } ")" ) .
<a id="ImportSpec">ImportSpec</a>       = [ "." | <a href="/Packages/package_clause.html#PackageName">PackageName</a> ] <a href="#ImportPath">ImportPath</a> .
<a id="ImportPath">ImportPath</a>       = <a href="/Lexical elements/string_literals.html#string_lit">string_lit</a> .
</pre>

The PackageName is used in [qualified identifiers](/Expressions/qualified_identifiers.html) to access exported identifiers of the package within the importing source file. It is declared in the [file block](/Blocks/). If the PackageName is omitted, it defaults to the identifier specified in the [package clause](/Packages/package_clause.html) of the imported package. If an explicit period (.) appears instead of a name, all the package's exported identifiers declared in that package's [package block](/Blocks/) will be declared in the importing source file's file block and must be accessed without a qualifier.

The interpretation of the ImportPath is implementation-dependent but it is typically a substring of the full file name of the compiled package and may be relative to a repository of installed packages.

Implementation restriction: A compiler may restrict ImportPaths to non-empty strings using only characters belonging to [Unicode](http://www.unicode.org/versions/Unicode6.3.0/)'s L, M, N, P, and S general categories (the Graphic characters without spaces) and may also exclude the characters !"#$%&'()*,:;<=>?[\]^`{|} and the Unicode replacement character U+FFFD.

Assume we have compiled a package containing the package clause package math, which exports function Sin, and installed the compiled package in the file identified by `"lib/math"`. This table illustrates how Sin is accessed in files that import the package after the various types of import declaration.

```go
Import declaration          Local name of Sin

import   "lib/math"         math.Sin
import m "lib/math"         m.Sin
import . "lib/math"         Sin
```

An import declaration declares a dependency relation between the importing and imported package. It is illegal for a package to import itself, directly or indirectly, or to directly import a package without referring to any of its exported identifiers. To import a package solely for its side-effects (initialization), use the [blank](/Declarations%20and%20scope/blank_identifier.html) identifier as explicit package name:

```go
import _ "lib/math"
```
