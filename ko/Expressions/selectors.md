# Selectors

For a [primary expression](/Expressions/primary_expressions.html) x that is not a [package name](/Packages/package_clause.html), the *selector expression*

```go
x.f
```

denotes the field or method f of the value x (or sometimes \*x; see below). The identifier f is called the (field or method) *selector*; it must not be the [blank identifier](/Declarations%20and%20scope/blank_identifier.html). The type of the selector expression is the type of f. If x is a package name, see the section on [qualified identifiers](/Expressions/qualified_identifiers.html).

A selector f may denote a field or method f of a type T, or it may refer to a field or method f of a nested [embedded field](/Types/struct_types.html) of T. The number of embedded fields traversed to reach f is called its *depth* in T. The depth of a field or method f declared in T is zero. The depth of a field or method f declared in an embedded field A in T is the depth of f in A plus one.

The following rules apply to selectors:

  * For a value x of type T or *T where T is not a pointer or interface type, x.f denotes the field or method at the shallowest depth in T where there is such an f. If there is not exactly [one f](/Declarations%20and%20scope/uniqueness_of_identifiers.html) with shallowest depth, the selector expression is illegal.
  * For a value x of type I where I is an interface type, x.f denotes the actual method with name f of the dynamic value of x. If there is no method with name f in the [method set](/Types/method_sets.html) of I, the selector expression is illegal.
  * As an exception, if the type of x is a named pointer type and (*x).f is a valid selector expression denoting a field (but not a method), x.f is shorthand for (*x).f.
  * In all other cases, x.f is illegal.
  * If x is of pointer type and has the value nil and x.f denotes a struct field, assigning to or evaluating x.f causes a [run-time panic](/Run-time%20panics/).
  * If x is of interface type and has the value nil, [calling](/Expressions/calls.html) or [evaluating](/Expressions/method_values.html) the method x.f causes a [run-time panic](/Run-time%20panics/).

For example, given the declarations:

```go
type T0 struct {
    x int
}

func (*T0) M0()

type T1 struct {
    y int
}

func (T1) M1()

type T2 struct {
    z int
    T1
    *T0
}

func (*T2) M2()

type Q *T2

var t T2     // with t.T0 != nil
var p *T2    // with p != nil and (*p).T0 != nil
var q Q = p
```

one may write:

```go
t.z          // t.z
t.y          // t.T1.y
t.x          // (*t.T0).x

p.z          // (*p).z
p.y          // (*p).T1.y
p.x          // (*(*p).T0).x

q.x          // (*(*q).T0).x        (*q).x is a valid field selector

p.M0()       // ((*p).T0).M0()      M0 expects *T0 receiver
p.M1()       // ((*p).T1).M1()      M1 expects T1 receiver
p.M2()       // p.M2()              M2 expects *T2 receiver
t.M2()       // (&t).M2()           M2 expects *T2 receiver, see section on Calls
```

but the following is invalid:

```go
q.M0()       // (*q).M0 is valid but not a field selector
```