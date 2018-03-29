# [Source file organization](#source-file-organization)

Each source file consists of a package clause defining the package to which it belongs, followed by a possibly empty set of import declarations that declare packages whose contents it wishes to use, followed by a possibly empty set of declarations of functions, types, variables, and constants.

<pre>
<a id="SourceFile">SourceFile</a>       = <a href="/Packages/package_clause.html#PackageClause">PackageClause</a> ";" { <a href="/Packages/import_declarations.html#ImportDecl">ImportDecl</a> ";" } { <a href="/Declarations and scope/#TopLevelDecl">TopLevelDecl</a> ";" } .
</pre>
