# [slice 타입](#slice-types)

 * Go 버전: 1.9
 * 원문: [Slice types](https://golang.org/ref/spec#Slice_types)
 * 번역자: Jhonghee Park (@jhonghee)

슬라이즈는 *내재하는* array의 연속된 한 조각에 대해 서술한 것이며 그 array로 부터 숫자가 매겨진 연속된 요소들에 접근을 하게 해 준다. 슬라이스 타입은 그 요소 타입으로 구성된 array들의 모든 슬라이스를 포함하는 집합을 의미한다. 초기화 되지 않은 슬라이스의 값은 `nil`이다.

<pre>
<a id="SliceType">SliceType</a> = "[" "]" <a href="/Types/array_types.html#ElementType">ElementType</a> .
</pre>

array와 마찬가지로, 슬라이스도 인덱스로 접근할 수 있고 길이도 가진다. 슬라이스 s의 길이는 내장함수 [len](/Built-in%20functions/length_and_capacity.html)를 통해 얻을 수 있다; array와는 다르게 실행 도중에도 바뀔 수 있다. 요소들은 0에서 len(s) - 1까지의 정수 [인덱스들](/Expressions/index_expressions.html)을 통해 방문할 수 있다. 주어진 요소에 대해 슬라이스의 인덱스는 내재하는 array의 동일한 요소의 인덱스보다 작을 수 있다.

한번 초기화된 슬라이스는 그 요소들을 붙잡고 있는 내재된 array과 항상 결합되게 된다. 그러므로 슬라이스는 내재하는 array와 저장공간을 공유하며 같은 array의 다른 슬라이스와도 마찬가지이다; 대조적으로, 서로 다른 array들은 각각 특유의 저장공간을 가진다. 

내재하는 array는 슬라이스의 끝을 넘어서도 계속될 수 있다. *수용력(capapcity)*은 그러한 범위에 대한 계량이다: 슬라이스의 길이와 슬라이스의 경계를 넘어서 있는 구역의 길이의 합이다; 수용력(capacity)과 같은 길이의 슬라이스는 원래의 슬라이스로 부터 [슬라이싱(slicing)](/Expressions/slice_expressions.html)을 사용해 새로운 슬라이스로 만들 수 있다. 슬라이스의 수용력(capacity)는 내장 함수 [cap(a)](/Built-in%20functions/length_and_capacity.html)를 가지고 산출할 수 있다.

주어진 요소 타입 T의 새롭게 초기화된 슬라이스는 내장 함수 [make](/Built-in%20functions/making_slices,_maps_and_channels.html)를 사용해 만들 수 있는데, make는 슬라이스 타입과 길이, 그리고 선택적으로 수용력(capacity)을 인자로 받는다. make로 만든 슬라이스는 항상 새로운 array를 은밀히 할당하고 반환된 슬라이스가 가리키도록 한다. 즉, 다음을 실행하면

```
make([]T, length, capacity)
```

array를 할당하고 [슬라이싱(slicing)](/Expressions/slice_expressions.html)으로 슬라이스를 만든 것과 같은 슬라이스를 생산하게 되어서, 다음의 두 표현식은 동일하다:

```
make([]int, 50, 100)
new([100]int)[0:50]
```

array와 마찬가지로, 슬라이스도 항상 일차원이긴 하지만 고차원 객체들이 만들어 지도록 조립될 수 있다. array들의 array들인 경우, 내부의 array는 만들어 지는 과정에서, 항상 같은 길이다; 하지만 슬라이스의 슬라이스 (혹은 슬라이스의 array들)인 경우는, 내부 슬라이스의 길이가 역동적으로(dynamically) 다를 수 있다. 더우기, 내부의 슬라이스들은 반드시 개별적으로 초기화되어야 한다.