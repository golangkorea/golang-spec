# Declarations and scope

A *declaration* binds a non-[blank](/Declarations%20and%20scope/blank_identifier.html) identifier to a [constant](/Declarations%20and%20scope/constant_declarations.html), [type](/Declarations%20and%20scope/type_declarations.html), [variable](/Declarations%20and%20scope/variable_declarations.html), [function](/Declarations%20and%20scope/function_declarations.html), [label](/Statements/labeled_statements.html), or [package](/Packages/import_declarations.html). Every identifier in a program must be declared. No identifier may be declared twice in the same block, and no identifier may be declared in both the file and package block.

The [blank identifier](/Declarations%20and%20scope/blank_identifier.html) may be used like any other identifier in a declaration, but it does not introduce a binding and thus is not declared. In the package block, the identifier `init` may only be used for [init function](/Program%20initialization%20and%20execution/package_initialization.html) declarations, and like the blank identifier it does not introduce a new binding.

<pre>
<a id="Declaration">Declaration</a>   = <a href="/Declarations%20and%20scope/constant_declarations.html#ConstDecl">ConstDecl</a> | <a href="/Declarations%20and%20scope/type_declarations.html#TypeDecl">TypeDecl</a> | <a href="/Declarations%20and%20scope/variable_declarations.html#VarDecl">VarDecl</a> .
<a id="TopLevelDecl">TopLevelDecl</a>  = <a href="#Declaration">Declaration</a> | <a href="/Declarations%20and%20scope/function_declarations.html#FunctionDecl">FunctionDecl</a> | <a href="/Declarations%20and%20scope/method_declarations.html#MethodDecl">MethodDecl</a> .
</pre>

The *scope* of a declared identifier is the extent of source text in which the identifier denotes the specified constant, type, variable, function, label, or package.

Go is lexically scoped using [blocks](/Blocks/):

  1. The scope of a [predeclared identifier](/Declarations%20and%20scope/predeclared_identifiers.html) is the universe block.
  2. The scope of an identifier denoting a constant, type, variable, or function (but not method) declared at top level (outside any function) is the package block.
  3. The scope of the package name of an imported package is the file block of the file containing the import declaration.
  4. The scope of an identifier denoting a method receiver, function parameter, or result variable is the function body.
  5. The scope of a constant or variable identifier declared inside a function begins at the end of the ConstSpec or VarSpec (ShortVarDecl for short variable declarations) and ends at the end of the innermost containing block.
  6. The scope of a type identifier declared inside a function begins at the identifier in the TypeSpec and ends at the end of the innermost containing block.

An identifier declared in a block may be redeclared in an inner block. While the identifier of the inner declaration is in scope, it denotes the entity declared by the inner declaration.

The [package clause](/Packages/package_clause.html) is not a declaration; the package name does not appear in any scope. Its purpose is to identify the files belonging to the same [package](/Packages/) and to specify the default package name for import declarations.
