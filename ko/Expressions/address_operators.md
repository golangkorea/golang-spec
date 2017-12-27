# Address operators

For an operand x of type T, the address operation &x generates a pointer of type *T to x. The operand must be addressable, that is, either a variable, pointer indirection, or slice indexing operation; or a field selector of an addressable struct operand; or an array indexing operation of an addressable array. As an exception to the addressability requirement, x may also be a (possibly parenthesized) [composite literal](/Expressions/composite_literals.html). If the evaluation of x would cause a [run-time panic](/Run-time%20panics/), then the evaluation of &x does too.

For an operand x of pointer type *T, the pointer indirection *x denotes the [variable](/Variables/) of type T pointed to by x. If x is nil, an attempt to evaluate *x will cause a [run-time panic](/Run-time%20panics/).

    &x
    &a[f(2)]
    &Point{2, 3}
    *p
    *pf(x)
    
    var x *int = nil
    *x   // causes a run-time panic
    &*x  // causes a run-time panic