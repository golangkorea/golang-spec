# Deletion of map elements

The built-in function delete removes the element with key k from a [map](/Types/map_types.html) m. The type of k must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to the key type of m.

```go
delete(m, k)  // remove element m[k] from map m
```

If the map m is nil or the element m[k] does not exist, delete is a no-op.
