# [크기와 얼라인먼트 보증(Size and alignment guarantees)](#size-and-alignment-guarantees)

* Go 버전: 1.9
* 원문: [Size and alignment guarantees](https://golang.org/ref/spec#Size_and_alignment_guarantees)
* 번역자: Jhonghee Park(@jhonghee)

For the [numeric types](/Types/numeric_types.html), the following sizes are guaranteed:

[숫자 타입들(numeric types)](/Types/numeric_types.html)에 대해서, 다음과 같은 크기가 보증된다:

```
type                                  바이트수

byte, uint8, int8                     1
uint16, int16                         2
uint32, int32, float32                4
uint64, int64, float64, complex64     8
complex128                           16
```

The following minimal alignment properties are guaranteed:

  1. For a variable `x` of any type: `unsafe.Alignof(x)` is at least 1.
  2. For a variable `x` of struct type: `unsafe.Alignof(x)` is the largest of all the values `unsafe.Alignof(x.f)` for each field `f` of `x`, but at least 1.
  3. For a variable `x` of array type: `unsafe.Alignof(x)` is the same as the alignment of a variable of the array's element type.

다음과 같은 최소의 얼라인먼트 특성이 보증된다:

 1. 어떤 타입의 변수 `x`에 대해: `unsafe.Alignof(x)`는 적어도 1 이상 이다.
 2. 구조체 타입의 변수 `x`에 대해: `unsafe.Alignof(x)`는 `x`의 각 필드 `f`에 대한 `unsafe.Alignof(x.f)` 값들 중 최대값이나, 적어도 1 이상 이다.
 3. 정렬(array) 타입의 변수 `x`에 대해: `unsafe.Alignof(x)`는 정렬의 요소 타입의 변수의 얼라인먼트와 같다.

A struct or array type has size zero if it contains no fields (or elements, respectively) that have a size greater than zero. Two distinct zero-size variables may have the same address in memory.

필드 타입과 요소 타입의 크기가 0보다 크다 할지라도 구조체나 정렬(array) 타입은 필드가 없을 경우 (정렬(array)내 요소가 없을 경우) 크기가 0(zero)이다. 크기가 0(zero)인 서로 다른 두 변수들은 메모리내 같은 주소를 가질 수도 있다.