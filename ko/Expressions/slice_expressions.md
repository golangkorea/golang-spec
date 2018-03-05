# [슬라이스 표현식](#slice-expressions)

슬라이스 표현식은 문자열, 배열, 배열을 가리키는 포인터 혹은 슬라이스로부터 부분 문자열이나 슬라이스를 만들어낸다. 여기에는 두 가지 변형이 있다: 하한과 상한을 지정하는 단순한 형식, 그리고 용량에 대한 경계를 지정하는 완전한 형식

## [단순 슬라이스 표현식](#simple-slice-expressions)

문자열, 배열, 배열을 가리키는 포인터 혹은 슬라이스인 `a`에 대한 기본 표현식

```go
a[low : high]
```

부분 문자열 혹은 슬라이스를 만든다. *색인* `low`와 `high`는 피연산자 `a`의 어떤 요소들이 결과에 나타날지를 선택한다. 그 결과는 배열 `a`를 슬라이싱한 후에 0에서 시작하여 길이가 `high - low`인 색인을 갖는다. 

```go
a := [5]int{1, 2, 3, 4, 5}
s := a[1:4]
```

슬라이스 `s`는 `[]int` 타입에 길이 3, 용량 4와 이에 해당하는 요소들을 갖는다.

```go
s[0] == 2
s[1] == 3
s[2] == 4
```

편의를 위해 색인이 생략될 수도 있다. `low` 색인이 생략되면 기본 값은 0이며; `high` 색인이 생략되면 기본 값은 슬라이스된 피연산자의 길이다.

```go
a[2:]  // a[2 : len(a)]와 동일
a[:3]  // a[0 : 3]와 동일
a[:]   // a[0 : len(a)]와 동일
```

`a`가 배열을 가리키는 포인터라면, `a[low : high]`는 `(*a)[low : high]`의 축약이다.

For arrays or strings, the indices are *in range* if `0 <= low <= high <= len(a)`, otherwise they are *out of range*. For slices, the upper index bound is the slice capacity `cap(a)` rather than the length. A [constant](/Constants/) index must be non-negative and representable by a value of type `int`; for arrays or constant strings, constant indices must also be in range. If both indices are constant, they must satisfy `low <= high`. If the indices are out of range at run time, a [run-time panic](/Run-time%20panics/) occurs.

Except for [untyped strings](/Constants/), if the sliced operand is a string or slice, the result of the slice operation is a non-constant value of the same type as the operand. For untyped string operands the result is a non-constant value of type `string`. If the sliced operand is an array, it must be [addressable](/Expressions/address_operators.md) and the result of the slice operation is a slice with the same element type as the array.

If the sliced operand of a valid slice expression is a `nil` slice, the result is a `nil` slice. Otherwise, the result shares its underlying array with the operand.

## [완전 슬라이스 표현식](#full-slice-expressions)

배열, 배열을 가리키는 포인터 혹은 슬라이스 `a` (문자열은 아님)에 대한 기본 표현식

```go
a[low : high : max]
```

constructs a slice of the same type, and with the same length and elements as the simple slice expression `a[low : high]`. Additionally, it controls the resulting slice's capacity by setting it to `max - low`. Only the first index may be omitted; it defaults to 0. After slicing the array `a`

```go
a := [5]int{1, 2, 3, 4, 5}
t := a[1:3:5]
```

슬라이스 `t`는 `[]int` 타입에 길이 2, 용량 4이며, 이에 해당하는 원소들을 갖는다.

```go
t[0] == 2
t[1] == 3
```

As for simple slice expressions, if `a` is a pointer to an array, `a[low : high : max]` is shorthand for `(*a)[low : high : max]`. If the sliced operand is an array, it must be [addressable](/Expressions/address_operators.md).

The indices are *in range* if `0 <= low <= high <= max <= cap(a)`, otherwise they are *out of range*. A [constant](/Constants/) index must be non-negative and representable by a value of type `int`; for arrays, constant indices must also be in range. If multiple indices are constant, the constants that are present must be in range relative to each other. If the indices are out of range at run time, a [run-time panic](/Run-time%20panics/) occurs.
