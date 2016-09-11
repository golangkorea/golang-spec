# Type declarations

A type declaration binds an identifier, the *type name*, to a new type that has the same [underlying type](/Types/) as an existing type, and operations defined for the existing type are also defined for the new type. The new type is [different](/Properties%20of%20types%20and%20values/type_identity.html) from the existing type.

<pre>
<a id="TypeDecl">TypeDecl</a>     = "type" ( <a href="#TypeSpec">TypeSpec</a> | "(" { <a href="#TypeSpec">TypeSpec</a> ";" } ")" ) .
<a id="TypeSpec">TypeSpec</a>     = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> <a href="/Types/#Type">Type</a> .
</pre>

```
type IntArray [16]int

type (
	Point struct{ x, y float64 }
	Polar Point
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

The declared type does not inherit any [methods](/Declarations%20and%20scope/method_declarations.html) bound to the existing type, but the [method set](/Types/method_sets.html) of an interface type or of elements of a composite type remains unchanged:

```
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
// Lock and Unlock bound to its anonymous field Mutex.
type PrintableMutex struct {
	Mutex
}

// MyBlock is an interface type that has the same method set as Block.
type MyBlock Block
```

A type declaration may be used to define a different boolean, numeric, or string type and attach methods to it:

```
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