# [map 타입(Map types)](#map-types)

* Go 버전: 1.9
* 원문: [Map types](https://golang.org/ref/spec#Map_types)
* 번역자: Jhonghee Park (@jhonghee)

A map is an unordered group of elements of one type, called the element type, indexed by a set of unique keys of another type, called the key type. The value of an uninitialized map is `nil`.

map은 순서없이 구성된 단일 타입 요소들의 그룹이며, 요소의 타입은 요소 타입(element type)이라고 부른다. map에서는 키 타입(key type)의 고유한 *키*를 이용해 요소에 접근할 수 있다. 초기화되지 않은 map의 값은 `nil`이다.

<pre>
<a id="MapType">MapType</a>     = "map" "[" <a href="#KeyType">KeyType</a> "]" <a href="/Types/array_types.html#ElementType">ElementType</a> .
<a id="KeyType">KeyType</a>     = <a href="/Types/#Type">Type</a> .
</pre>

The [comparison operators](/Expressions/comparison_operators.html) == and != must be fully defined for operands of the key type; thus the key type must not be a function, map, or slice. If the key type is an interface type, these comparison operators must be defined for the dynamic key values; failure will cause a [run-time panic](/Run-time%20panics/).


피연산자인 키의 타입은 [비교 연산자](/Expressions/comparison_operators.html)인 `==`와 `!=`을 완전히 지원해야 한다; 때문에 키 타입으로 함수, map, 또는 슬라이스를 사용할 수 없다. 키가 인터페이스 타입인 경우는 동적으로 정해지는 값들에 대해 비교 연산자들을 사용할 수 있어야 한다; 그렇지 않을 경우 [런타임 패닉](/Run-time%20panics/)을 초래한다.

```
map[string]int
map[*T]struct{ x, y float64 }
map[string]interface{}
```

The number of map elements is called its length. For a map m, it can be discovered using the built-in function [len](/Built-in%20functions/length_and_capacity.html) and may change during execution. Elements may be added during execution using [assignments](/Statements/assignments.html) and retrieved with [index expressions](/Expressions/index_expressions.html); they may be removed with the [delete](/Built-in%20functions/deletion_of_map_elements.html) built-in function.

map `m`에 대한 길이는 내장 함수인 [len](/Built-in%20functions/length_and_capacity.html)을 이용해 구할 수 있으며, 이 길이는 프로그램 실행 중 변경될 수 있다. 프로그램 실행 중 [할당(assignments)](/Statements/assignments.html)을 이용해 새로운 요소를 추가할 수 있으며, [인덱스 식(index expressions)](/Expressions/index_expressions.html)을 이용해 요소에 접근할 수 있다; 내장 함수인 [`delete`](/Built-in%20functions/deletion_of_map_elements.html)를 사용해 요소를 삭제할 수도 있다.

A new, empty map value is made using the built-in function [make](/Built-in%20functions/making_slices,_maps_and_channels.html), which takes the map type and an optional capacity hint as arguments:

내장 함수인 [`make`](/Built-in%20functions/making_slices,_maps_and_channels.html)를 이용해 새로운 empty map을 만들 수 있다. make 함수의 인자로는 map 타입을 전달하고, 추가인자로 용량(capacity)을 사용할 수 있다.


```
make(map[string]int)
make(map[string]int, 100)
```

The initial capacity does not bound its size: maps grow to accommodate the number of items stored in them, with the exception of `nil` maps. A `nil` map is equivalent to an empty map except that no elements may be added.

map의 크기는 초기에 설정된 용량(capacity)에 의해 결정되지 않는다. `nil` map인 경우를 제외하고는 저장된 요소의 수에 맞게 map의 크기는 늘어난다. 새로운 요소를 추가할 수 없는 것을 제외하면 `nil` map은 empty map과 동일하다.
