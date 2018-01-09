# [Package initialization](#package-initialization)

Within a package, package-level variables are initialized in *declaration order* but after any of the variables they *depend* on.

More precisely, a package-level variable is considered *ready for initialization* if it is not yet initialized and either has no [initialization expression](/Declarations and scope/variable_declarations.html) or its initialization expression has no dependencies on uninitialized variables. Initialization proceeds by repeatedly initializing the next package-level variable that is earliest in declaration order and ready for initialization, until there are no variables ready for initialization.

If any variables are still uninitialized when this process ends, those variables are part of one or more initialization cycles, and the program is not valid.

The declaration order of variables declared in multiple files is determined by the order in which the files are presented to the compiler: Variables declared in the first file are declared before any of the variables declared in the second file, and so on.

Dependency analysis does not rely on the actual values of the variables, only on lexical *references* to them in the source, analyzed transitively. For instance, if a variable x's initialization expression refers to a function whose body refers to variable y then x depends on y. Specifically:

- A reference to a variable or function is an identifier denoting that variable or function.
- A reference to a method `m` is a [method value](/Expressions/method_values.html) or [method expression](/Expressions/method_expressions.html) of the form `t.m`, where the (static) type of `t` is not an interface type, and the method `m` is in the [method set](/Types/method_sets.html) of `t`. It is immaterial whether the resulting function value `t.m` is invoked.
- A variable, function, or method `x` depends on a variable `y` if `x`'s initialization expression or body (for functions and methods) contains a reference to `y` or to a function or method that depends on `y`.

Dependency analysis is performed per package; only references referring to variables, functions, and methods declared in the current package are considered.

For example, given the declarations

    var (
        a = c + b
        b = f()
        c = f()
        d = 3
    )
    
    func f() int {
        d++
        return d
    }
    

the initialization order is d, b, c, a.

Variables may also be initialized using functions named init declared in the package block, with no arguments and no result parameters.

    func init() { … }
    

Multiple such functions may be defined, even within a single source file. The `init` identifier is not [declared](/Declarations and scope/) and thus `init` functions cannot be referred to from anywhere in a program.

A package with no imports is initialized by assigning initial values to all its package-level variables followed by calling all `init` functions in the order they appear in the source, possibly in multiple files, as presented to the compiler. If a package has imports, the imported packages are initialized before initializing the package itself. If multiple packages import a package, the imported package will be initialized only once. The importing of packages, by construction, guarantees that there can be no cyclic initialization dependencies.

Package initialization—variable initialization and the invocation of `init` functions—happens in a single goroutine, sequentially, one package at a time. An `init` function may launch other goroutines, which can run concurrently with the initialization code. However, initialization always sequences the `init` functions: it will not invoke the next one until the previous one has returned.

To ensure reproducible initialization behavior, build systems are encouraged to present multiple files belonging to the same package in lexical file name order to a compiler.