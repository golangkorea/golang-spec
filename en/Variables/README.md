# [Variables](#variables)

A variable is a storage location for holding a value. The set of permissible values is determined by the variable's *[type](/Types/)*.

A [variable declaration](/Declarations%20and%20scope/variable_declarations.html) or, for function parameters and results, the signature of a [function declaration](/Declarations%20and%20scope/function_declarations.html) or [function literal](/Expressions/function_literals.html) reserves storage for a named variable. Calling the built-in function [new](/Built-in%20functions/allocation.html) or taking the address of a [composite literal](/Expressions/composite_literals.html) allocates storage for a variable at run time. Such an anonymous variable is referred to via a (possibly implicit) [pointer indirection](/Expressions/address_operators.html).

*Structured* variables of [array](/Types/array_types.html), [slice](/Types/slice_types.html), and [struct](/Types/struct_types.html) types have elements and fields that may be [addressed](/Expressions/address_operators.html) individually. Each such element acts like a variable.

The *static type* (or just *type*) of a variable is the type given in its declaration, the type provided in the `new` call or composite literal, or the type of an element of a structured variable. Variables of interface type also have a distinct *dynamic type*, which is the concrete type of the value assigned to the variable at run time (unless the value is the predeclared identifier `nil`, which has no type). The dynamic type may vary during execution but values stored in interface variables are always [assignable](/Properties%20of%20types%20and%20values/assignability.html) to the static type of the variable.

```
var x interface{}  // x is nil and has static type interface{}
var v *T           // v has value nil, static type *T
x = 42             // x has value 42 and dynamic type int
x = v              // x has value (*T)(nil) and dynamic type *T
```

A variable's value is retrieved by referring to the variable in an [expression](/Expressions/); it is the most recent value [assigned](/Statements/assignments.html) to the variable. If a variable has not yet been assigned a value, its value is the [zero value](/Program%20initialization%20and%20execution/the_zero_value.html) for its type.