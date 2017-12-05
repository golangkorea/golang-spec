# Array types

# Array 타입

* 원문 : [Array types](https://golang.org/ref/spec#Array_types)
* 번역자 : [연규민](@voidsatisfaction)

An array is a numbered sequence of elements of a single type, called the element type. The number of elements is called the length and is never negative.

Array는 번호가 붙은, 요소의 타입(element type)이라고 불리는, 단일 타입 요소의 연속이다. 요소들의 개수는 길이(length) 라고 불리며 절대로 음수가 될 수 없다.

<pre>
<a id="ArrayType">ArrayType</a>   = "[" <a href="#ArrayLength">ArrayLength</a> "]" <a href="#ElementType">ElementType</a> .
<a id="ArrayLength">ArrayLength</a> = [Expression](/Expressions/) .
<a id="ElementType">ElementType</a> = [Type](/Types/) .
</pre>

The length is part of the array's type; it must evaluate to a non-negative [constant](/Constants/) representable by a value of type `int`. The length of array a can be discovered using the built-in function [len](/Built-in%20functions/length_and_capacity.html). The elements can be addressed by integer [indices](/Expressions/index_expressions.html) 0 through `len(a)-1`. Array types are always one-dimensional but may be composed to form multi-dimensional types.

길이는 Array 타입의 일부이다; 이는 음수가 아닌 `int`타입의 [상수](/Constants/)로 평가(evaluate)되어야 한다. Array의 길이는 내장 함수인 [len](/Built-in%20functions/length_and_capacity.html)으로 구할 수 있다. 요소들은 0 부터 `len(a)-1`까지의 정수 [인덱스들](/Expressions/index_expressions.html)로 접근할 수 있다. Array 타입은 언제나 일차원적(one-dimensional)이나, 다차원적(multi-dimensional) 타입을 형성하기 위해서 합성될 수 있다.

```
[32]byte
[2*N] struct { x, y int32 }
[1000]*float64
[3][5]int
[2][2][2]float64  // same as [2]([2]([2]float64))
```

```
[32]byte
[2*N] struct { x, y int32 }
[1000]*float64
[3][5]int
[2][2][2]float64  // 다음과 같음 [2]([2]([2]float64))
```
