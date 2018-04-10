# [합성 리터럴](#composite-literals)

합성 리터럴은 struct, 배열, 슬라이스, map 타입의 값으로 구성되며, 매번 평가될 때마다 새로운 값이 만들어진다. 합성 리터럴은 리터럴 타입과 함께 요소들의 리스트가 `{ }` 안에 나열되는 형태로 구성된다. 각 요소 앞에 해당 요소와 관련된 키(key)를 추가할 수 있다.

<pre>
<a id="CompositeLit">CompositeLit</a>  = <a href="#LiteralType">LiteralType</a> <a href="#LiteralValue">LiteralValue</a> .
<a id="LiteralType">LiteralType</a>   = <a href="/Types/struct_types.html#StructType">StructType</a> | <a href="/Types/array_types.html#ArrayType">ArrayType</a> | "[" "..." "]" <a href="/Types/array_types.html#ElementType">ElementType</a> | <a href="/Types/slice_types.html#SliceType">SliceType</a> | <a href="/Types/map_types.html#MapType">MapType</a> | <a href="/Types/#TypeName">TypeName</a> .
<a id="LiteralValue">LiteralValue</a>  = "{" [ <a href="#ElementList">ElementList</a> [ "," ] ] "}" .
<a id="ElementList">ElementList</a>   = <a href="#KeyedElement">KeyedElement</a> { "," <a href="#KeyedElement">KeyedElement</a> } .
<a id="KeyedElement">KeyedElement</a>  = [ <a href="#Key">Key</a> ":" ] <a href="#Element">Element</a> .
<a id="Key">Key</a>           = <a href="#FieldName">FieldName</a> | <a href="/Expressions/operators.html#Expression">Expression</a> | <a href="#LiteralValue">LiteralValue</a> .
<a id="FieldName">FieldName</a>     = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
<a id="Element">Element</a>       = <a href="/Expressions/operators.html#Expression">Expression</a> | <a href="#LiteralValue">LiteralValue</a> .
</pre>

LiteralType의 내재 타입은 struct, 배열, 슬라이스, 또는 map 타입이어야 한다 (타입이 TypeName으로 주어질 때를 제외하고는 문법에 이러한 제약이 적용된다). 요소와 키의 타입은 리터럴 타입의 관련 필드, 요소, 타입에 [할당 가능해야](/Properties%20of%20types%20and%20values/assignability.html)한다; 이때, 추가적인 변환은 발생하지 않는다. map 리터럴의 키, struct 리터럴의 필드명, 배열과 슬라이스 리터럴의 인덱스를 키(key)의 용도로 사용할 수 있다. map 리터럴은 모든 요소가 키를 가져야 한다. 여러 요소가 같은 필드명이나 같은 상수 키 값을 가지면 에러가 발생한다. 상수가 아닌 map 키에 대해서는 [평가 순서](/Expressions/order_of_evaluation.html) 섹션을 참조하라.

struct 리터럴에는 아래의 규칙이 적용된다:

  * 키는 struct 타입 안에 선언된 필드 이름이어야 한다.
  * 키를 포함하지 않은 요소 리스트는 필드가 선언된 순서대로 각 struct 필드에 해당하는 요소를 나열해야 한다.
  * 만약 키를 가지고 있는 요소가 1개라도 있다면, 모든 요소는 키가 있어야 한다.
  * 키를 포함하는 요소들의 리스트가 각 struct 필드에 대한 요소를 반드시 가질 필요는 없다. 생략된 필드들은 해당 필드에 대해 제로값을 얻는다.
  * 리터럴에서 요소 리스트를 생략할 수 있다; 이 경우, 리터럴은 해당 타입에 대한 제로값으로 평가된다.
  * 다른 패키지에 속한 struct의 엑스포트되지 않은 필드의 요소를 지정하면 에러가 발생한다.

아래의 선언문을 이용해

```go
type Point3D struct { x, y, z float64 }
type Line struct { p, q Point3D }
```

다음과 같이 코드를 작성할 수 있다.

```go
origin := Point3D{}                            // Point3D는 제로값
line := Line{origin, Point3D{y: -4, z: 12.3}}  // line.q.x는 제로값
```

배열과 슬라이스 리터럴에는 아래의 규칙이 적용된다:

  * 각 요소는 배열 안에서 자신의 위치를 나타내는 정수 인덱스를 가진다.
  * 키를 가지는 요소는 키를 인덱스로 사용한다. 키는 `int` 타입의 값으로 나타낼 수 있는 음수가 아닌 상수여야 한다;  타입이 있다면 정수 타입이어야 한다.
  * 키가 없는 요소는 바로 이전 요소의 인덱스에 1을 더한다. 만약 첫번째 요소가 키가 없으면, 그 요소의 인덱스는 0이다.

합성 리터럴의 [주소를 이용해](/Expressions/address_operators.html) 리터럴의 값으로 초기화되는 고유 [변수](/Variables/)를 가리키는 포인터가 생성된다.

```go
var pointer *Point3D = &Point3D{y: 1000}
```

배열 리터럴의 길이는 리터럴 타입에서 지정된 길이다. 만약 리터럴 길이보다 요소의 갯수가 적다면, 남은 공간은 배열 요소 타입의 제로값으로 채워진다. 배열의 인덱스 범위 밖의 인덱스 값을 가진 요소를 제공하면 에러가 난다. `...` 표기법은 최대 요소 인덱스 + 1 의 배열 길이를 나타낸다.

```go
buffer := [10]string{}             // len(buffer) == 10
intSet := [6]int{1, 2, 3, 5}       // len(intSet) == 6
days := [...]string{"Sat", "Sun"}  // len(days) == 2
```

슬라이스 리터럴은 내재 배열 리터럴 전체를 나타낸다. 그러므로, 슬라이스의 길이와 용량은 최대 요소 인덱스 + 1 이 된다.  슬라이스 리터럴은 아래의 형태로 구성하며

```go
[]T{x1, x2, … xn}
```

슬라이스 리터럴은 배열에 대한 슬라이스 연산을 축약한 것이다: 

```go
tmp := [n]T{x1, x2, … xn}
tmp[0 : n]
```

배열, 슬라이스, map 타입 `T`의 합성 리터럴에 대해, 요소 또는 map 키가 합성 리터럴이고 이들의 타입이 `T`와 같다면 이들에 대한 리터럴 타입을 생략할 수 있다. 또한, 요소 또는 키가 합성 리터럴의 주소이고 이들의 타입이 `*T`라면, `&T`를 생략할 수 있다. 

```go
[...]Point{{1.5, -3.5}, {0, 0}}     // [...]Point{Point{1.5, -3.5}, Point{0, 0}}와 같다
[][]int{{1, 2, 3}, {4, 5}}          // [][]int{[]int{1, 2, 3}, []int{4, 5}}와 같다
[][]Point{{{0, 1}, {1, 2}}}         // [][]Point{[]Point{Point{0, 1}, Point{1, 2}}}와 같다
map[string]Point{"orig": {0, 0}}    // map[string]Point{"orig": Point{0, 0}}와 같다.
map[Point]string{{0, 0}: "orig"}    // map[Point]string{Point{0, 0}: "orig"}와 같다.

type PPoint *Point
[2]*Point{{1.5, -3.5}, {}}          // [2]*Point{&Point{1.5, -3.5}, &Point{}}와 같다.
[2]PPoint{{1.5, -3.5}, {}}          // [2]PPoint{PPoint(&Point{1.5, -3.5}), PPoint(&Point{})}와 같다.
```

LiteralType의 TypeName 형태를 사용하는 합성 리터럴이 [키워드](/Lexical%20elements/keywords.html)와 "if", "for", "switch" 구문 블록을 시작하는 중괄호 사이의 피연산자로 나타나고 합성 리터럴이 괄호, 각괄호, 중괄호 안에 없는 경우 파싱이 모호해질 수 있다. 이러한 현상은 거의 발생하지 않지만, 리터럴의 시작하는 중괄호가 구문 블록 시작으로 잘못 파싱될 수 있다. 이러한 모호성을 피하려면 합성 리터럴을 반드시 괄호 안에서 사용해야 한다.

```go
if x == (T{a,b,c}[i]) { … }
if (x == T{a,b,c}[i]) { … }
```

유효한 배열, 슬라이스, map 리터럴의 예제들:


```go
// 소수의 리스트
primes := []int{2, 3, 5, 7, 9, 2147483647}

// ch가 모음이면 vowels[ch] 는 true
vowels := [128]bool{'a': true, 'e': true, 'i': true, 'o': true, 'u': true, 'y': true}

// 배열 [10]float32{-1, 0, 0, 0, -0.1, -0.1, 0, 0, 0, -1}
filter := [10]float32{-1, 4: -0.1, -0.1, 9: -1}

// 평균율 음계 (A4 = 440Hz)에 대해 주파수를 Hz로 표시
noteFrequency := map[string]float32{
    "C0": 16.35, "D0": 18.35, "E0": 20.60, "F0": 21.83,
    "G0": 24.50, "A0": 27.50, "B0": 30.87,
}
```
