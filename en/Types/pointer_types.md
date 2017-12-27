# [Pointer types](#pointer-types)
 
A pointer type denotes the set of all pointers to [variables](/Variables/) of a given type, called the base *type* of the pointer. The value of an uninitialized pointer is `nil`.

<pre>
<a id="PointerType">PointerType</a> = "*" <a href="#BaseType">BaseType</a> .
<a id="BaseType">BaseType</a>    = <a href="/Types/#Type">Type</a> .
</pre>

```
*Point
*[4]int
```