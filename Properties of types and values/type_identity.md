# [타입 아이덴티티(Type identity)](#type-identity)

* Go 버전: 1.9
* 원문: [Type identity](https://golang.org/ref/spec#Type_identity)
* 번역자: Jhonghee Park (@jhonghee)

Two types are either identical or different.

두개의 타입은 동일하거나 다르다.

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

[정의된 타입(defined type)](/Declarations%20and%20scope/type_declarations.html#type-definitions)은 항상 다른 타입들과 다르다. 그렇지 않을 경우, 만약 타입 사이에서 [내재하는(underlying)](/Types/) 타입 리터럴이 구조적으로 동일하다면; 즉, 동일한 리터럴 구조와 상응하는 구성요소가 동일한 타입을 가지고 있다면 그 타입들은 동일하다. 자세하게 설명하자면:

 * 두개의 정렬(array) 타입은 만약 동일한 요소 타입과 동일한 길이를 가지고 있다면 동일한다.
 * 두개의 슬라이스(slice) 타입은 만약 동일한 요소 타입을 가지고 있다면 동일하다.
 * 두개의 구조체(struct) 타입은 만약 같은 순서로 필드들이 배치되고, 상응하는 필드의 명칭들이 동일하며, 동일한 타입과 동일한 태그들을 가지고 있다면 동일하다. 서로 다른 패키지내에 [엑스포트 되지않은(Non-exported)](/Declarations%20and%20scope/exported_identifiers.html) 필드의 이름들은 항상 다르다.
 * 두개의 포인터 타입은 만약 동일한 기본 타입(base types)를 가지고 있으면 동일하다.
 * 두개의 함수 타입은 가변성인자 함수(variadic)이든 아니든 만약 같은 수의 인자와 반환값, 상응하는 인자의 타입과 반환값의 타입이 같으면 동일하다. 인자와 반환 값의 명칭들은 똑같을 필요가 없다.
 * 두개의 인터페이스 타입은 만약 동일한 명칭과 함수 타입의 메소드로 구성된 동일한 메소드의 집합을 가지고 있다면 동일하다. 서로 다른 패키지내에 [엑스포트 되지않은(Non-exported)](/Declarations%20and%20scope/exported_identifiers.html) 메소드의 이름들은 항상 다르다.
 * 두개의 맵(map) 타입은 만약 동일한 타입의 키(key)와 값을 갖고 있다면 동일하다.
 * 두개의 채널(channel) 타입은 만약 동일한 타입의 값과 동일한 방향성을 갖고 있다면 동일하다.

Given the declarations

아래 주어진 선언문에서

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

B0 and C0
[]int and []int
struct{ a, b *T5 } and struct{ a, b *T5 }
func(x int, y float64) *[]string, func(int, float64) (result *[]string), and A5
```

`B0` and `B1` are different because they are new types created by distinct <a href="#Type_definitions">type definitions</a>; `func(int, float64) *B0` and `func(x int, y float64) *[]string` are different because `B0` is different from `[]string`.

`B0`와 `B1`은 서로 다른 이유는 독특한 [타입 정의(type definitions)](/Declarations%20and%20scope/type_declarations.html#type-definitions)들로 만들어지 새로운 타입들이기 때문이다; `B0`이 `[]string`과 다르기 때문에 `func(int, float64) *B0`과 `func(x int, y float64) *[]string`은 서로 다르다.