# [Map types](#map-types)

A map is an unordered group of elements of one type, called the element type, indexed by a set of unique keys of another type, called the key type. The value of an uninitialized map is `nil`.

<pre>
<a id="MapType">MapType</a>     = "map" "[" <a href="#KeyType">KeyType</a> "]" <a href="/Types/array_types.html#ElementType">ElementType</a> .
<a id="KeyType">KeyType</a>     = <a href="/Types/#Type">Type</a> .
</pre>

The [comparison operators](/Expressions/comparison_operators.html) == and != must be fully defined for operands of the key type; thus the key type must not be a function, map, or slice. If the key type is an interface type, these comparison operators must be defined for the dynamic key values; failure will cause a [run-time panic](/Run-time%20panics/).

    map[string]int
    map[*T]struct{ x, y float64 }
    map[string]interface{}
    

The number of map elements is called its length. For a map m, it can be discovered using the built-in function [len](/Built-in%20functions/length_and_capacity.html) and may change during execution. Elements may be added during execution using [assignments](/Statements/assignments.html) and retrieved with [index expressions](/Expressions/index_expressions.html); they may be removed with the [delete](/Built-in%20functions/deletion_of_map_elements.html) built-in function.

A new, empty map value is made using the built-in function [make](/Built-in%20functions/making_slices,_maps_and_channels.html), which takes the map type and an optional capacity hint as arguments:

    make(map[string]int)
    make(map[string]int, 100)
    

The initial capacity does not bound its size: maps grow to accommodate the number of items stored in them, with the exception of `nil` maps. A `nil` map is equivalent to an empty map except that no elements may be added.