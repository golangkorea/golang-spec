# [타입 아이덴티티(Type identity)](#type-identity)

* Go 버전: 1.9
* 원문: [Type identity](https://golang.org/ref/spec#Type_identity)
* 번역자: Jhonghee Park (@jhonghee)

Two types are either identical or different.

2개의 타입은 같거나(identical) 다르다.

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

[타입 정의를 이용해 만든 타입(defined type)](/Declarations%20and%20scope/type_declarations.html#type-definitions)은 항상 다른 타입과 다르다. 그 밖의 타입은 [내재(underlying)](/Types/) 타입 리터럴이 구조적으로 동일하다면 두 개의 타입이 서로 같다고 말할 수 있다; 즉, 리터럴 구조와 상응하는 구성요소가 같다면 같은 타입이라고 할 수 있다. 자세하게 설명하자면:

 * 2개의 array 타입은 요소 타입과 배열 길이가 같으면 서로 같다.
 * 2개의 슬라이스 타입은 요소 타입이 같다면 서로 같다. 
 * 2개의 struct 타입은 필드 순서가 같고, 상응하는 필드의 이름, 타입, 태그가 같으면 서로 같다. 서로 다른 패키지의 [엑스포트 되지 않은(Non-exported)](/Declarations%20and%20scope/exported_identifiers.html) 필드 이름들은 항상 다르다.
 * 2개의 포인터 타입은 기본 타입(base types)이 같으면 서로 같다.
 * 2개의 함수 타입은 매개변수 갯수, 반환 값 갯수, 상응하는 매개변수의 타입과 반환 값의 타입이 같으면 서로 같다. 2개의 함수는 모두 variadic 함수거나 둘 다 variadic 함수가 아니여도 된다. 매개변수와 반환 값의 이름들은 달라도 된다.
 * 2개의 interface 타입은 같은 이름과 같은 함수 타입으로 구성된 메서드의 집합이 같으면 서로 같다. 서로 다른 패키지내에 [엑스포트 되지 않은(Non-exported)](/Declarations%20and%20scope/exported_identifiers.html) 메서드의 이름들은 항상 다르다. 메서드의 순서는 상관없다.
 * 2개의 map 타입은 키(key) 타입과 값 타입이 같으면 서로 같다.
 * 2개의 channel 타입은 값 타입과 방향성(direction)이 같으면 서로 같다.

Given the declarations

아래 선언문에서

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

다음의 타입들은 동일하다.

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


`B0`와 `B1`이 서로 다른 이유는 별도의 [타입 정의(type definitions)](/Declarations%20and%20scope/type_declarations.html#type-definitions)를 이용해 생성한 새로운 타입들이기 때문이다; `B0`이 `[]string`과 다르기 때문에 `func(int, float64) *B0`과 `func(x int, y float64) *[]string`은 서로 다르다.

