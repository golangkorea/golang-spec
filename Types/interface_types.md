# Interface types

An interface type specifies a [method set](/Types/method_sets.html) called its *interface*. A variable of interface type can store a value of any type with a method set that is any superset of the interface. Such a type is said to *implement the interface*. The value of an uninitialized variable of interface type is `nil`.

<pre>
<a id="InterfaceType">InterfaceType</a>      = "interface" "{" { <a href="#MethodSpec">MethodSpec</a> ";" } "}" .
<a id="MethodSpec">MethodSpec</a>         = <a href="#MethodName">MethodName</a> <a href="/Types/function_types.html#Signature">Signature</a> | <a href="#InterfaceTypeName">InterfaceTypeName</a> .
<a id="MethodName">MethodName</a>         = <a href="/Lexical%20elements/identifiers.html">identifier</a> .
<a id="InterfaceTypeName">InterfaceTypeName</a>  = <a href="/Types/#TypeName">TypeName</a> .
</pre>

As with all method sets, in an interface type, each method must have a [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html) non-[blank](/Declarations%20and%20scope/blank_identifier.html) name.

// A simple File interface
interface {
	Read(b Buffer) bool
	Write(b Buffer) bool
	Close()
}
More than one type may implement an interface. For instance, if two types S1 and S2 have the method set

```
func (p T) Read(b Buffer) bool { return … }
func (p T) Write(b Buffer) bool { return … }
func (p T) Close() { … }
```

(where T stands for either S1 or S2) then the File interface is implemented by both S1 and S2, regardless of what other methods S1 and S2 may have or share.

A type implements any interface comprising any subset of its methods and may therefore implement several distinct interfaces. For instance, all types implement the *empty interface*:

```
interface{}
```

Similarly, consider this interface specification, which appears within a [type declaration](/Declarations%20and%20scope/type_declarations.html) to define an interface called Locker:

```
type Locker interface {
	Lock()
	Unlock()
}
```

If S1 and S2 also implement

```
func (p T) Lock() { … }
func (p T) Unlock() { … }
```

they implement the Locker interface as well as the `File` interface.

An interface T may use a (possibly qualified) interface type name E in place of a method specification. This is called *embedding* interface E in T; it adds all (exported and non-exported) methods of E to the interface T.

```
type ReadWriter interface {
	Read(b Buffer) bool
	Write(b Buffer) bool
}

type File interface {
	ReadWriter  // same as adding the methods of ReadWriter
	Locker      // same as adding the methods of Locker
	Close()
}

type LockedFile interface {
	Locker
	File        // illegal: Lock, Unlock not unique
	Lock()      // illegal: Lock not unique
}
```

An interface type T may not embed itself or any interface type that embeds T, recursively.

```
// illegal: Bad cannot embed itself
type Bad interface {
	Bad
}

// illegal: Bad1 cannot embed itself using Bad2
type Bad1 interface {
	Bad2
}
type Bad2 interface {
	Bad1
}
```