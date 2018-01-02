# [String types](#string-types)

A *string type* represents the set of string values. A string value is a (possibly empty) sequence of bytes. Strings are immutable: once created, it is impossible to change the contents of a string. The predeclared string type is `string`.

The length of a string s (its size in bytes) can be discovered using the built-in function [len](/Built-in%20functions/length_and_capacity.html). The length is a compile-time constant if the string is a constant. A string's bytes can be accessed by integer [indices](/Expressions/index_expressions.html) 0 through `len(s)-1`. It is illegal to take the address of such an element; if `s[i]` is the i'th byte of a string, `&s[i]` is invalid.