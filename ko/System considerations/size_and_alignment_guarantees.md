# [Size and alignment guarantees](#size-and-alignment-guarantees)

For the [numeric types](/Types/numeric_types.html), the following sizes are guaranteed:

    type                                  size in bytes
    
    byte, uint8, int8                     1
    uint16, int16                         2
    uint32, int32, float32                4
    uint64, int64, float64, complex64     8
    complex128                           16
    

The following minimal alignment properties are guaranteed:

1. For a variable `x` of any type: `unsafe.Alignof(x)` is at least 1.
2. For a variable `x` of struct type: `unsafe.Alignof(x)` is the largest of all the values `unsafe.Alignof(x.f)` for each field `f` of `x`, but at least 1.
3. For a variable `x` of array type: `unsafe.Alignof(x)` is the same as the alignment of a variable of the array's element type.

A struct or array type has size zero if it contains no fields (or elements, respectively) that have a size greater than zero. Two distinct zero-size variables may have the same address in memory.