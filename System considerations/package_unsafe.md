# Package unsafe

The built-in package `unsafe`, known to the compiler, provides facilities for low-level programming including operations that violate the type system. A package using `unsafe` must be vetted manually for type safety and may not be portable. The package provides the following interface:

```
package unsafe

type ArbitraryType int  // shorthand for an arbitrary Go type; it is not a real type
type Pointer *ArbitraryType

func Alignof(variable ArbitraryType) uintptr
func Offsetof(selector ArbitraryType) uintptr
func Sizeof(variable ArbitraryType) uintptr
```

A Pointer is a [pointer type](/Types/pointer_types.html) but a `Pointer` value may not be [dereferenced](/Expressions/address_operators.html). Any pointer or value of [underlying type](/Types/) `uintptr` can be converted to a type of underlying type `Pointer` type and vice versa. The effect of converting between `Pointer` and `uintptr` is implementation-defined.

```
var f float64
bits = *(*uint64)(unsafe.Pointer(&f))

type ptr unsafe.Pointer
bits = *(*uint64)(ptr(&f))

var p ptr = nil
```

The functions `Alignof` and `Sizeof` take an expression x of any type and return the alignment or size, respectively, of a hypothetical variable v as if v was declared via `var v = x`.

The function `Offsetof` takes a (possibly parenthesized) [selector](/Expressions/selectors.html) `s.f`, denoting a field `f` of the struct denoted by `s` or `*s`, and returns the field offset in bytes relative to the struct's address. If `f` is an [embedded field](/Types/struct_types.html), it must be reachable without pointer indirections through fields of the struct. For a struct `s` with field `f`:

```
uintptr(unsafe.Pointer(&s)) + unsafe.Offsetof(s.f) == uintptr(unsafe.Pointer(&s.f))
```

Computer architectures may require memory addresses to be *aligned*; that is, for addresses of a variable to be a multiple of a factor, the variable's type's *alignment*. The function `Alignof` takes an expression denoting a variable of any type and returns the alignment of the (type of the) variable in bytes. For a variable `x`:

```
uintptr(unsafe.Pointer(&x)) % unsafe.Alignof(x) == 0
```

Calls to `Alignof`, `Offsetof`, and `Sizeof` are compile-time constant expressions of type `uintptr`.