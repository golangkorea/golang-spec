# [슬라이스 복사와 슬라이스에 추가하기](#appending-to-and-copying-slices)

`append`와 `copy` 내장 함수는 슬라이스의 연산들에 많이 쓰인다. 인자들에 의해 참조되는 메모리의 중첩 여부는 두 함수의 결과에 아무런 영향을 미치지 않는다.

[가변 인자 함수](/Types/function_types.html)인 `append`는 슬라이스 타입(`S`로 표기)의 `s`에 대해 0개 이상의 값 `x`를 추가하고 그 결과로 `S` 타입의 슬라이스를 반환한다. 값 `x`는 `...T` 타입의 매개 변수로 전달된다. 여기에서 `T`는 `S`의 [요소 타입](/Types/slice_types.html)이고 각 `x` 값에는 [매개 변수 전달 규칙](/Expressions/passing_arguments_to__parameters.html)이 적용된다. 또한, 첫 번째 인자로 `[]byte` 타입에 할당할 수 있는 것을 사용하고, 두 번째 인자는 문자열 타입 뒤에 `...`가 추가된 형태로 `append`를 사용할 수도 있다.  이러한 형태의 `append`는 문자열의 바이트를 추가할 때 사용한다.

```go
append(s S, x ...T) S  // T는 S의 요소 타입이다.
```

`s`의 용량이 추가적인 값들을 수용하기에 충분히 크지 않다면, `append`는 기존의 슬라이스 요소들과 새로운 값들을 담기에 충분히 큰 내재 배열을 새롭게 할당한다. `s`의 용량이 충분할 경우에는 내재 배열을 재사용한다.

```go
s0 := []int{0, 0}
s1 := append(s0, 2)                // 단일 요소 추가      s1 == []int{0, 0, 2}
s2 := append(s1, 3, 5, 7)          // 다중 요소 추가    s2 == []int{0, 0, 2, 3, 5, 7}
s3 := append(s2, s0...)            // 슬라이스 추가              s3 == []int{0, 0, 2, 3, 5, 7, 0, 0}
s4 := append(s3[3:6], s3[2:]...)   // 중첩되는 슬라이스 추가    s4 == []int{3, 5, 7, 2, 3, 5, 7, 0, 0}

var t []interface{}
t = append(t, 42, 3.1415, "foo")   //                             t == []interface{}{42, 3.1415, "foo"}

var b []byte
b = append(b, "bar"...)            // 문자열 추가      b == []byte{'b', 'a', 'r' }
```

`copy` 함수는 원본(source)에 해당하는 `src`의 슬라이스 요소들을 대상(destination)에 해당하는 `dst`로 복사하고 복사된 요소들의 개수를 반환한다. 두 인자들은 [같은](/Properties%20of%20types%20and%20values/type_identity.html) 요소 타입 `T`여야 하며, `[]T` 타입의 슬라이스에 [할당 가능](/Properties%20of%20types%20and%20values/assignability.html)해야 한다. 복사된 요소들의 개수는 `len(src)`와 `len(dst)` 중에서 최소값이 된다. 또한 `copy`는 원본에 해당하는 인자로 문자열 타입을 사용하고, 대상에 해당하는 인자로 `[]byte` 타입에 할당 가능한 타입을 사용할 수 있다. 문자열의 바이트를 바이트 슬라이스에 복사할 때 이러한 형태의 `copy`를 사용할 수 있다.

```go
copy(dst, src []T) int
copy(dst []byte, src string) int
```

예제:

```go
var a = [...]int{0, 1, 2, 3, 4, 5, 6, 7}
var s = make([]int, 6)
var b = make([]byte, 5)
n1 := copy(s, a[0:])            // n1 == 6, s == []int{0, 1, 2, 3, 4, 5}
n2 := copy(s, s[2:])            // n2 == 4, s == []int{2, 3, 4, 5, 4, 5}
n3 := copy(b, "Hello, World!")  // n3 == 5, b == []byte("Hello")
```
