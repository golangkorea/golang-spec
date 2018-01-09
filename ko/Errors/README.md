# [Errors](#errors)

The predeclared type `error` is defined as

```go
type error interface {
    Error() string
}
```

It is the conventional interface for representing an error condition, with the nil value representing no error. For instance, a function to read data from a file might be defined:

```go
func Read(f *File, b []byte) (n int, err error)
```