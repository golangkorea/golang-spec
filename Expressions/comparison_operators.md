# [비교 연산자(Comparison operators)](#comparison-operators)

* Go 버전: 1.9
* 원문: [Comparison operators](https://golang.org/ref/spec#Comparison_operators)
* 번역자: Jhonghee Park (@jhonghee)

Comparison operators compare two operands and yield an untyped boolean value.

비교 연산자들은 2개의 피 연산자들을 비교한 다음 미지정 타입의(untyped) 불리언 값을 생산한다.

```
==    equal
!=    not equal
<     less
<=    less or equal
>     greater
>=    greater or equal
```

```
==    같은
!=    같지 않은
<     더 적은
<=    더 적거나 같은
>     더 큰
>=    더 크거나 같은
```

In any comparison, the first operand must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to the type of the second operand, or vice versa.

어떤 비교 연산에서든, 첫번째 피연산자는 두번째 피연산자의 타입에 [할당 가능(assignable)](/Properties%20of%20types%20and%20values/assignability.html)해야 하며, 그 반대도 마찬가지이다.

The equality operators == and != apply to operands that are *comparable*. The ordering operators <, <=, >, and >= apply to operands that are *ordered*. These terms and the result of the comparisons are defined as follows:

  * Boolean values are comparable. Two boolean values are equal if they are either both true or both false.
  * Integer values are comparable and ordered, in the usual way.
  * Floating point values are comparable and ordered, as defined by the IEEE-754 standard.
  * Complex values are comparable. Two complex values u and v are equal if both real(u) == real(v) and imag(u) == imag(v).
  * String values are comparable and ordered, lexically byte-wise.
  * Pointer values are comparable. Two pointer values are equal if they point to the same variable or if both have value nil. Pointers to distinct [zero-size](/System%20considerations/size_and_alignment_guarantees.html) variables may or may not be equal.
  * Channel values are comparable. Two channel values are equal if they were created by the same call to [make](/making_slices,_maps_and_channels.html) or if both have value `nil`.
  * Interface values are comparable. Two interface values are equal if they have [identical](/Properties%20of%20types%20and%20values/type_identity.html) dynamic types and equal dynamic values or if both have value nil.
  * A value `x` of non-interface type `X` and a value `t` of interface type `T` are comparable when values of type `X` are comparable and `X` implements `T`. They are equal if `t`'s dynamic type is identical to `X` and `t`'s dynamic value is equal to `x`.
  * Struct values are comparable if all their fields are comparable. Two struct values are equal if their corresponding non-[blank](/Declarations%20and%20scope/blank_identifier.html) fields are equal.
  * Array values are comparable if values of the array element type are comparable. Two array values are equal if their corresponding elements are equal.

*서로 비교할 수 있는* 피연산자들에 대등 연산자인 `==`와 `!=`가 적용된다. 순서 연산자인 `<`, `<=`, `>`, 그리고 `>=`는 *순서를 정할 수 있는* 피연산자들에 적용된다. 비교의 조건들과 결과에 대해서는 다음과 같이 정의한다:

 * 불리언 값들은 비교할 수 있다. 2개의 불리언 값은 둘 다 `true`이던지 `false`일 때 같다.
 * 정수 값들은, 잘 알려져 있듯이, 비교할 수 있고 순서도 있다.
 * 부동 소수점 값들은, IEEE-754 표준에 정의된 바에 따라, 비교할 수 있고 순서도 있다.
 * 복소수 값들은 비교 가능하다. 2개의 복소수 값들, `u`와 `v`는 만약 두 조건, `real(u) == real(v)`와 `imag(u) == imag(v)`가 만족하면 같다.
 * string 값들은 어휘적으로 바이트 단위로 비교할 수 있고 순서도 있다.
 * 포인터 값들은 비교 가능하다. 2개의 포인터 값이 같은 변수를 가리키고 있던지 둘 다 `nil`이면 같다. 서로 다르며 [크기가 0인(zero-size)](/System%20considerations/size_and_alignment_guarantees.html) 변수들을 가리키는 포인터들은 같을 수도 있고 다를 수도 있다.
 * 채널 값들은 비교 가능하다. 만약 2개의 채널이 같은 [make](/making_slices,_maps_and_channels.html)의 호출을 통해 만들어 졌다면 같고, 둘 다 `nil`값을 갖고 있다면 같다.
 * 인터페이스 값들은 비교 가능하다. 2개의 인터페이스는 [동일한](/Properties%20of%20types%20and%20values/type_identity.html) 동적 타입을 가지고 있고 같은 동적 값을 가지고 있을 때 서로 같다. 둘 다 `nil`값을 갖고 있어도 같다.
 * 인터페이스가 아닌 타입 `X`의 값 `x`와 인터페이스 타입 `T`의 값 `t`는 `X`가 비교 가능한 타입이며 `T`를 구현하고 있는 경우 서로 비교할 수 있다.
 * struct 값들은 필드가 모두 비교 가능한 경우에 비교연산에 사용할 수 있다. 2개의 struct 값들 사이에 [blank 식별자](/Declarations%20and%20scope/blank_identifier.html)가 아닌 상응하는 필드들이 서로 같은 값이면 같다.
 * 배열 값들은 만약 배열의 요소가 비교 가능한 타입이면 배열의 비교연산도 가능하다. 2개의 배열값 사이에는 만약 상응하는 요소들이 같다면 같다.

A comparison of two interface values with identical dynamic types causes a [run-time panic](/Run-time%20panics/) if values of that type are not comparable. This behavior applies not only to direct interface value comparisons but also when comparing arrays of interface values or structs with interface-valued fields.

동일한 동적 타입을 갖는 2개의 인터페이스 값들이 비교했을 때 만약 이 값들이 비교 가능한 값들이 아니면 [런타임 panic](/Run-time%20panics/)을 초래한다. 이러한 일들은 인터페이스간의 직접적인 비교뿐만 아니라 인터페이스 값을 지닌 배열을 비교할 때와 인터페이스 값을 갖고 있는 필드를 지닌 struct간의 비교에도 적용된다.

Slice, map, and function values are not comparable. However, as a special case, a slice, map, or function value may be compared to the predeclared identifier nil. Comparison of pointer, channel, and interface values to nil is also allowed and follows from the general rules above.

슬라이스, map, 그리고 함수 값들은 비교할 수 없다. 하지만, 특별한 경우로, 하나의 슬라이스, map, 그리고 함수 값은 미리 선언된 식별자 `nil`과 비교할 수 있다. 포인터, 채널, 그리고 인터페이스 값을 `nil`과 비교하는 것도 허용되며 위에 명시된 일반적인 규칙을 따른다.

```
const c = 3 < 4            // c is the untyped boolean constant true

type MyBool bool
var x, y int
var (
	// The result of a comparison is an untyped boolean.
	// The usual assignment rules apply.
	b3        = x == y // b3 has type bool
	b4 bool   = x == y // b4 has type bool
	b5 MyBool = x == y // b5 has type MyBool
)
```

```
const c = 3 < 4            // c는 미지정 타입의 불리언 상수 true

type MyBool bool
var x, y int
var (
	// 비교연산의 결과는 미지정 타입의 불리언이다.
	// 보통의 할당 규칙들이 적용된다.
	b3        = x == y // b3는 타입 bool을 갖는다
	b4 bool   = x == y // b4는 타입 bool을 갖는다
	b5 MyBool = x == y // b5는 타입 MyBool를 갖는다
)
```