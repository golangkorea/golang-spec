# Making slices, maps and channels

The built-in function make takes a type T, which must be a slice, map or channel type, optionally followed by a type-specific list of expressions. It returns a value of type T (not *T). The memory is initialized as described in the section on [initial values](/Program initialization and execution/the_zero_value.html).

```
Call             Type T     Result

make(T, n)       slice      slice of type T with length n and capacity n
make(T, n, m)    slice      slice of type T with length n and capacity m

make(T)          map        map of type T
make(T, n)       map        map of type T with initial space for n elements

make(T)          channel    unbuffered channel of type T
make(T, n)       channel    buffered channel of type T, buffer size n
```

The size arguments n and m must be of integer type or untyped. A [constant](/Constants/) size argument must be non-negative and representable by a value of type int. If both n and m are provided and are constant, then n must be no larger than m. If n is negative or larger than m at run time, a [run-time panic](/Run-time panics/) occurs.

```
s := make([]int, 10, 100)       // slice with len(s) == 10, cap(s) == 100
s := make([]int, 1e3)           // slice with len(s) == cap(s) == 1000
s := make([]int, 1<<63)         // illegal: len(s) is not representable by a value of type int
s := make([]int, 10, 0)         // illegal: len(s) > cap(s)
c := make(chan int, 10)         // channel with a buffer size of 10
m := make(map[string]int, 100)  // map with initial space for 100 elements
```