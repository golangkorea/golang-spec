# [Type declarations](#type-declarations)

A type declaration binds an identifier, the *type name*, to a <a href="#Types">type</a>.
Type declarations come in two forms: alias declarations and type definitions.

<pre>
<a id="TypeDecl">TypeDecl</a> = "type" ( <a href="#TypeSpec">TypeSpec</a> | "(" { (<a href="#TypeSpec">TypeSpec</a> ";" } ")" ) .
<a id="TypeSpec">TypeSpec</a> = <a href="#AliasDecl">AliasDecl</a> | <a href="#TypeDef">TypeDef</a> .
</pre>

## [Alias declarations](#alias-declarations)

An alias declaration binds an identifier to the given type.

<pre>
<a id="AliasDecl">AliasDecl</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> "=" <a href="#Type">Type</a> .
</pre>

Within the [scope](/Declarations%20and%20scope/) of the identifier, it serves as an *alias* for the type.

```go
type (
	nodeList = []*Node  // nodeList and []*Node are identical types
	Polar    = polar    // Polar and polar denote identical types
)
```

## [Type definitions](#type-definitions)

A type definition creates a new, distinct type with the same [underlying type](/Types/) and operations as the given type, and binds an identifier to it.

<pre>
<a id="TypeDef">TypeDef</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> <a href="/Types/#Type">Type</a> .
</pre>

The new type is called a *defined type*.
It is [different](Properties%20of%20types%20and%20values/type_identity.html) from any other type, including the type it is created from.

```go
type (
	Point struct{ x, y float64 }  // Point and struct{ x, y float64 } are different types
	polar Point                   // polar and Point denote different types
)

type TreeNode struct {
	left, right *TreeNode
	value *Comparable
}

type Block interface {
	BlockSize() int
	Encrypt(src, dst []byte)
	Decrypt(src, dst []byte)
}
```
A defined type may have [methods](/Declarations%20and%20scope/method_declarations.html) associated with it.
It does not inherit any methods bound to the given type, but the [method set](/Types/method_sets.html) of an interface type or of elements of a composite type remains unchanged:

```go
// A Mutex is a data type with two methods, Lock and Unlock.
type Mutex struct         { /* Mutex fields */ }
func (m *Mutex) Lock()    { /* Lock implementation */ }
func (m *Mutex) Unlock()  { /* Unlock implementation */ }

// NewMutex has the same composition as Mutex but its method set is empty.
type NewMutex Mutex

// The method set of the base type of PtrMutex remains unchanged,
// but the method set of PtrMutex is empty.
type PtrMutex *Mutex

// The method set of *PrintableMutex contains the methods
// Lock and Unlock bound to its embedded field Mutex.
type PrintableMutex struct {
	Mutex
}

// MyBlock is an interface type that has the same method set as Block.
type MyBlock Block
```

Type definitions may be used to define different boolean, numeric, or string types and associate methods with them:

```go
type TimeZone int

const (
	EST TimeZone = -(5 + iota)
	CST
	MST
	PST
)

func (tz TimeZone) String() string {
	return fmt.Sprintf("GMT%+dh", tz)
}
```
