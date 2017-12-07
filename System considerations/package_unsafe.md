# [unsafe 패키지(Package unsafe)](#package-unsafe)

* Go 버전: 1.9
* 원문: [Package unsafe](https://golang.org/ref/spec#Package_unsafe)
* 번역자: Jhonghee Park(@jhonghee)

The built-in package `unsafe`, known to the compiler, provides facilities for low-level programming including operations that violate the type system. A package using `unsafe` must be vetted manually for type safety and may not be portable. The package provides the following interface:

Go 컴파일러에 숙지된 바와 같이, `unsafe` 내장 패키지는 타입 시스템을 위반하는 연산을 포함한 낮은 레벨(low-level)의 프로그래밍을 수월하게 하는 기능을 제공한다. `unsafe`를 사용하는 패키지는 타입 안전성에 대해 프로그래머가 직접 면밀히 조사해야 하며 코드가 포터블(portable)하지 않다. 패키지는 다음과 같은 인터페이스를 제공한다:

```
package unsafe

type ArbitraryType int  // arbitrary Go type의 줄임말; 실제 타입이 아님.
type Pointer *ArbitraryType

func Alignof(variable ArbitraryType) uintptr
func Offsetof(selector ArbitraryType) uintptr
func Sizeof(variable ArbitraryType) uintptr
```

A Pointer is a [pointer type](/Types/pointer_types.html) but a `Pointer` value may not be [dereferenced](/Expressions/address_operators.html). Any pointer or value of [underlying type](/Types/) `uintptr` can be converted to a type of underlying type `Pointer` type and vice versa. The effect of converting between `Pointer` and `uintptr` is implementation-defined.

Pointer는 [포인터 타입(pointer type)](/Types/pointer_types.html)이며 `Pointer`값은 [디레퍼런스(dereferenced)](/Expressions/address_operators.html)될 수 없다. [내재 타입(underlying type)](/Types/)이 `uintptr`인 어떤 포인터나 값은 `Pointer` 타입으로 변환될 수 있고, 반대 방향의 변환도 가능하다. `Pointer`와 `uintptr`간 변환의 효과는 구현시 정의(implementation-defined)된다.

```
var f float64
bits = *(*uint64)(unsafe.Pointer(&f))

type ptr unsafe.Pointer
bits = *(*uint64)(ptr(&f))

var p ptr = nil
```

The functions `Alignof` and `Sizeof` take an expression x of any type and return the alignment or size, respectively, of a hypothetical variable v as if v was declared via `var v = x`.

`Alignof`와 `Sizeof` 함수들은 어떤 타입의 x 표현식을 받아서, 마치 `var v = x`로 v가 선언된 것 처럼 가설적인 변수 v의 얼라인먼트(alignment)와 크기를 각각 돌려준다.

The function `Offsetof` takes a (possibly parenthesized) [selector](/Expressions/selectors.html) `s.f`, denoting a field `f` of the struct denoted by `s` or `*s`, and returns the field offset in bytes relative to the struct's address. If `f` is an [embedded field](/Types/struct_types.html), it must be reachable without pointer indirections through fields of the struct. For a struct `s` with field `f`:

`Offsetof` 함수는 구조체인 `s`나 `*s`의 필드를 의미하는 `f`를 (괄호가 사용되었을 가능성이 있는) [선택자 표현(selector)](/Expressions/selectors.html)인 `s.f`로 받아서 구조체 주소에 상대적인 필드의 오프셋(offset)을 바이트 단위로 돌려준다. 만약 `f`가 [임베드된 필드(embedded field)](/Types/struct_types.html)일 경우, 구조체의 필드들을 통한 포인터 인디렉션(pointer indirection) 없이 접근할 수 있어야 한다. 구조체 `s`의 필드 `f`에 대해:

```
uintptr(unsafe.Pointer(&s)) + unsafe.Offsetof(s.f) == uintptr(unsafe.Pointer(&s.f))
```

Computer architectures may require memory addresses to be *aligned*; that is, for addresses of a variable to be a multiple of a factor, the variable's type's *alignment*. The function `Alignof` takes an expression denoting a variable of any type and returns the alignment of the (type of the) variable in bytes. For a variable `x`:

어떤 컴퓨터 아키텍쳐들은 메모리 주소의 *정렬(aligned)*을 요구할 수도 있다; 즉, 변수의 주소들은 변수 타입의 *얼라인먼트(alignment)*라는 인자의 배수이어야 한다. `Alignof` 함수는 어떤 타입의 변수를 의미하는 표현식을 받아서 (그 타입의) 변수의 얼라인먼트를 바이트 단위로 돌려준다. 변수 `x`의 예를 들자면:


```
uintptr(unsafe.Pointer(&x)) % unsafe.Alignof(x) == 0
```

Calls to `Alignof`, `Offsetof`, and `Sizeof` are compile-time constant expressions of type `uintptr`.

`Alignof`, `Offsetof`, 그리고 `Sizeof` 함수들에 대한 호출은 `uintptr` 타입의 컴파일 타임(compile-time) 상수 표현들이다.