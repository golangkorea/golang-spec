# Iota

Within a [constant declaration](/Declarations%20and%20scope/constant_declarations.html), the predeclared identifier iota represents successive untyped integer [constants](/Constants/). It is reset to 0 whenever the reserved word const appears in the source and increments after each [ConstSpec](/Declarations%20and%20scope/constant_declarations.html#ConstSpec). It can be used to construct a set of related constants:

    const ( // iota is reset to 0
        c0 = iota  // c0 == 0
        c1 = iota  // c1 == 1
        c2 = iota  // c2 == 2
    )
    
    const ( // iota is reset to 0
        a = 1 << iota  // a == 1
        b = 1 << iota  // b == 2
        c = 3          // c == 3  (iota is not used but still incremented)
        d = 1 << iota  // d == 8
    )
    
    const ( // iota is reset to 0
        u         = iota * 42  // u == 0     (untyped integer constant)
        v float64 = iota * 42  // v == 42.0  (float64 constant)
        w         = iota * 42  // w == 84    (untyped integer constant)
    )
    
    const x = iota  // x == 0  (iota has been reset)
    const y = iota  // y == 0  (iota has been reset)
    

Within an ExpressionList, the value of each iota is the same because it is only incremented after each ConstSpec:

    const (
        bit0, mask0 = 1 << iota, 1<<iota - 1  // bit0 == 1, mask0 == 0
        bit1, mask1                           // bit1 == 2, mask1 == 1
        _, _                                  // skips iota == 2
        bit3, mask3                           // bit3 == 8, mask3 == 7
    )
    

This last example exploits the implicit repetition of the last non-empty expression list.