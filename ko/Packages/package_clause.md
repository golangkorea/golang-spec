# Package clause

A package clause begins each source file and defines the package to which the file belongs.

<pre>
<a id="PackageClause">PackageClause</a>  = "package" <a href="#PackageName">PackageName</a> .
<a id="PackageName">PackageName</a>    = <a href="/Lexical elements/identifiers.html#identifier">identifier</a> .
</pre>

The PackageName must not be the [blank identifier](/Declarations and scope/blank_identifier.html).

    package math
    

A set of files sharing the same PackageName form the implementation of a package. An implementation may require that all source files for a package inhabit the same directory.