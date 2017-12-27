# [Slice types](#slice-types)

A slice is a descriptor for a contiguous segment of an *underlying* array and provides access to a numbered sequence of elements from that array. A slice type denotes the set of all slices of arrays of its element type. The value of an uninitialized slice is `nil`.

<pre>
<a id="SliceType">SliceType</a> = "[" "]" <a href="/Types/array_types.html#ElementType">ElementType</a> .
</pre>

Like arrays, slices are indexable and have a length. The length of a slice s can be discovered by the built-in function [len](/Built-in%20functions/length_and_capacity.html); unlike with arrays it may change during execution. The elements can be addressed by integer [indices](/Expressions/index_expressions.html) 0 through len(s)-1. The slice index of a given element may be less than the index of the same element in the underlying array.

A slice, once initialized, is always associated with an underlying array that holds its elements. A slice therefore shares storage with its array and with other slices of the same array; by contrast, distinct arrays always represent distinct storage.

The array underlying a slice may extend past the end of the slice. The *capacity* is a measure of that extent: it is the sum of the length of the slice and the length of the array beyond the slice; a slice of length up to that capacity can be created by [slicing](/Expressions/slice_expressions.html) a new one from the original slice. The capacity of a slice a can be discovered using the built-in function [cap(a)](/Built-in%20functions/length_and_capacity.html).

A new, initialized slice value for a given element type T is made using the built-in function [make](/Built-in%20functions/making_slices,_maps_and_channels.html), which takes a slice type and parameters specifying the length and optionally the capacity. A slice created with make always allocates a new, hidden array to which the returned slice value refers. That is, executing

```
make([]T, length, capacity)
```

produces the same slice as allocating an array and [slicing](/Expressions/slice_expressions.html) it, so these two expressions are equivalent:

```
make([]int, 50, 100)
new([100]int)[0:50]
```

Like arrays, slices are always one-dimensional but may be composed to construct higher-dimensional objects. With arrays of arrays, the inner arrays are, by construction, always the same length; however with slices of slices (or arrays of slices), the inner lengths may vary dynamically. Moreover, the inner slices must be initialized individually.