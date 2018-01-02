# Calls

Given an expression f of function type F,

    f(a1, a2, … an)
    

calls f with arguments a1, a2, … an. Except for one special case, arguments must be single-valued expressions [assignable](/Statements/assignments.html) to the parameter types of F and are evaluated before the function is called. The type of the expression is the result type of F. A method invocation is similar but the method itself is specified as a selector upon a value of the receiver type for the method.

    math.Atan2(x, y)  // function call
    var pt *Point
    pt.Scale(3.5)     // method call with receiver pt
    

In a function call, the function value and arguments are evaluated in the [usual order](/Expressions/order_of_evaluation.html). After they are evaluated, the parameters of the call are passed by value to the function and the called function begins execution. The return parameters of the function are passed by value back to the calling function when the function returns.

Calling a `nil` function value causes a [run-time panic](/Run-time%20panics/).

As a special case, if the return values of a function or method g are equal in number and individually assignable to the parameters of another function or method f, then the call f(g(*parameters_of_g*)) will invoke f after binding the return values of g to the parameters of f in order. The call of f must contain no parameters other than the call of g, and g must have at least one return value. If f has a final ... parameter, it is assigned the return values of g that remain after assignment of regular parameters.

    func Split(s string, pos int) (string, string) {
        return s[0:pos], s[pos:]
    }
    
    func Join(s, t string) string {
        return s + t
    }
    
    if Join(Split(value, len(value)/2)) != value {
        log.Panic("test fails")
    }
    

A method call x.m() is valid if the [method set](/Types/method_sets.html) of (the type of) x contains m and the argument list can be assigned to the parameter list of m. If x is [addressable](/Expressions/address_operators.html) and &x's method set contains m, x.m() is shorthand for (&x).m():

    var p Point
    p.Scale(3.5)
    

There is no distinct method type and there are no method literals.