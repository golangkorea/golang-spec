# Passing arguments to ... parameters {#passing-arguements-to-parameters}

If f is [variadic](/Types/function_types.html) with a final parameter p of type ...T, then within f the type of p is equivalent to type []T. If f is invoked with no actual arguments for p, the value passed to p is nil. Otherwise, the value passed is a new slice of type []T with a new underlying array whose successive elements are the actual arguments, which all must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to T. The length and capacity of the slice is therefore the number of arguments bound to p and may differ for each call site.

Given the function and calls

    func Greeting(prefix string, who ...string)
    Greeting("nobody")
    Greeting("hello:", "Joe", "Anna", "Eileen")
    

within Greeting, who will have the value nil in the first call, and []string{"Joe", "Anna", "Eileen"} in the second.

If the final argument is assignable to a slice type []T, it may be passed unchanged as the value for a ...T parameter if the argument is followed by .... In this case no new slice is created.

Given the slice s and call

    s := []string{"James", "Jasmine"}
    Greeting("goodbye:", s...)
    

within Greeting, who will have the same value as s with the same underlying array.