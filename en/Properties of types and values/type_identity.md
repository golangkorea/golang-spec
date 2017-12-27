# [Type identity](#type-identity)

Two types are either identical or different.

A <a href="#Type_definitions">defined type</a> is always different from any other type.
Otherwise, two types are identical if their <a href="#Types">underlying</a> type literals are
structurally equivalent; that is, they have the same literal structure and corresponding
components have identical types. In detail:

  * Two array types are identical if they have identical element types and the same array length.
  * Two slice types are identical if they have identical element types.
  * Two struct types are identical if they have the same sequence of fields, and if corresponding fields have the same names, and identical types, and identical tags. [Non-exported](/Declarations%20and%20scope/exported_identifiers.html) field names from different packages are always different.
  * Two pointer types are identical if they have identical base types.
  * Two function types are identical if they have the same number of parameters and result values, corresponding parameter and result types are identical, and either both functions are variadic or neither is. Parameter and result names are not required to match.
  * Two interface types are identical if they have the same set of methods with the same names and identical function types. [Non-exported](/Declarations%20and%20scope/exported_identifiers.html) method names from different packages are always different. The order of the methods is irrelevant.
  * Two map types are identical if they have identical key and value types.
  * Two channel types are identical if they have identical value types and the same direction.

Given the declarations

```
type (
	A0 []string
	A1 = A0
	A2 = struct{ a, b int }
	A3 = int
	A4 = func(A3, float64) *A0
	A5 = func(x int, _ float64) *[]string
)

type (
  B0 A0
  B1 []string
  B2 struct{ a, b int }
  B3 struct{ a, c int }
  B4 func(int, float64) *B0
  B5 func(x int, y float64) *A1
)

type	C0 = B0
```

these types are identical:

```
A0, A1, and []string
A2 and struct{ a, b int }
A3 and int
A4, func(int, float64) *[]string, and A5

B0, B0 and C0
[]int and []int
struct{ a, b *T5 } and struct{ a, b *T5 }
func(x int, y float64) *[]string, func(int, float64) (result *[]string), and A5
```

`B0` and `B1` are different because they are new types created by distinct <a href="#Type_definitions">type definitions</a>; `func(int, float64) *B0` and `func(x int, y float64) *[]string` are different because `B0` is different from `[]string`.