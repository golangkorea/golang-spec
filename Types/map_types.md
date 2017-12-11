# [map 타입(Map types)](#map-types)

* Go 버전: 1.9
* 원문: [Map types](https://golang.org/ref/spec#Map_types)
* 번역자: Jhonghee Park (@jhonghee)

A map is an unordered group of elements of one type, called the element type, indexed by a set of unique keys of another type, called the key type. The value of an uninitialized map is `nil`.

map은 하나의 요소 타입(element type)으로 순서없이 구성된 요소들의 그룹이며, 고유한 키 타입(key type)의 키들로 구성된 집합에 의해 색인된다. 초기화 되지 않은 map의 값은 `nil`이다.

<pre>
<a id="MapType">MapType</a>     = "map" "[" <a href="#KeyType">KeyType</a> "]" <a href="/Types/array_types.html#ElementType">ElementType</a> .
<a id="KeyType">KeyType</a>     = <a href="/Types/#Type">Type</a> .
</pre>

The [comparison operators](/Expressions/comparison_operators.html) == and != must be fully defined for operands of the key type; thus the key type must not be a function, map, or slice. If the key type is an interface type, these comparison operators must be defined for the dynamic key values; failure will cause a [run-time panic](/Run-time%20panics/).

[비교 연산자](/Expressions/comparison_operators.html)인 `==`과 `!=`는 피연산자에 대해서 완전히 정의되어야 한다: 때문에 키 타입으로 함수, map, 또는 슬라이스를 사용할 수 없다. 만약 키 타입이 인터페이스 타입일 경우에는, 동적 키 값들에 대해 비교 연산자들이 정의되어 있어야만 한다; 그렇지 않을 경우 [런타임 panic](/Run-time%20panics/)을 초래한다.

```
map[string]int
map[*T]struct{ x, y float64 }
map[string]interface{}
```

The number of map elements is called its length. For a map m, it can be discovered using the built-in function [len](/Built-in%20functions/length_and_capacity.html) and may change during execution. Elements may be added during execution using [assignments](/Statements/assignments.html) and retrieved with [index expressions](/Expressions/index_expressions.html); they may be removed with the [delete](/Built-in%20functions/deletion_of_map_elements.html) built-in function.

map 요소의 수를 map의 길이(length)라고 한다. 주어진 map `m`에 대해, 길이는 내장 함수인 [len](/Built-in%20functions/length_and_capacity.html)를 사용해 구할 수 있고 프로그램 실행중 달라질 수도 있다. 새로운 요소들이 실행중 [할당(assignments)](/Statements/assignments.html)을 통해 추가될 수 있고 [인덱스 표현(index expressions)](/Expressions/index_expressions.html)을 통해 추출될 수도 있다; 내장 함수인 [delete](/Built-in%20functions/deletion_of_map_elements.html)을 사용해 제거할 수도 있다.

A new, empty map value is made using the built-in function [make](/Built-in%20functions/making_slices,_maps_and_channels.html), which takes the map type and an optional capacity hint as arguments:

새로운 텅빈 map을 만들 때는 내장 함수인 [make](/Built-in%20functions/making_slices,_maps_and_channels.html)에 map 타입과 선택적으로 용량(capacity)를 인자로 사용한다.

```
make(map[string]int)
make(map[string]int, 100)
```

The initial capacity does not bound its size: maps grow to accommodate the number of items stored in them, with the exception of `nil` maps. A `nil` map is equivalent to an empty map except that no elements may be added.

초기 용량(capacity)은 map의 크기를 제한하지 않는다: `nil` map인 경우를 제외하고는 저장된 요소의 수에 맞게 map의 크기는 자란다. `nil` map은 새로운 요소를 추가할 수 없는 것을 제외하고는 텅빈(empty) map과 동일하다.
