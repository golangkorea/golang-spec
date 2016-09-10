# Type identity

Two types are either identical or different.

Two [named types](/Types/) are identical if their type names originate in the same [TypeSpec](/Declarations%20and%20scope/type_declarations.html). A named and an [unnamed type](/Types/) are always different. Two unnamed types are identical if the corresponding type literals are identical, that is, if they have the same literal structure and corresponding components have identical types. In detail:

  * Two array types are identical if they have identical element types and the same array length.
  * Two slice types are identical if they have identical element types.
  * Two struct types are identical if they have the same sequence of fields, and if corresponding fields have the same names, and identical types, and identical tags. Two anonymous fields are considered to have the same name. Lower-case field names from different packages are always different.
  * Two pointer types are identical if they have identical base types.
  * Two function types are identical if they have the same number of parameters and result values, corresponding parameter and result types are identical, and either both functions are variadic or neither is. Parameter and result names are not required to match.
  * Two interface types are identical if they have the same set of methods with the same names and identical function types. Lower-case method names from different packages are always different. The order of the methods is irrelevant.
  * Two map types are identical if they have identical key and value types.
  * Two channel types are identical if they have identical value types and the same direction.

Given the declarations

```
type (
	T0 []string
	T1 []string
	T2 struct{ a, b int }
	T3 struct{ a, c int }
	T4 func(int, float64) *T0
	T5 func(x int, y float64) *[]string
)
```

these types are identical:

```
T0 and T0
[]int and []int
struct{ a, b *T5 } and struct{ a, b *T5 }
func(x int, y float64) *[]string and func(int, float64) (result *[]string)
```

T0 and T1 are different because they are named types with distinct declarations; `func(int, float64) *T0` and `func(x int, y float64) *[]string` are different because T0 is different from `[]string`.