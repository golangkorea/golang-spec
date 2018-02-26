# [합성 리터럴](#composite-literals)

합성 리터럴은 구조체, 배열, 슬라이스, 그리고 맵의 값을 구성하며, 매번 평가될 때 마다 새로운 값이 만들어 진다. 리터럴의 타입뒤로 여러 요소들의 리스트를 중괄호로 묶어 이루어 진다. 각 요소는 상응하는 키가 선택적으로 앞에 놓일 수 있다. 

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

LiteralType의 내재 타입은 구조체, 배열, 슬라이스, 혹은 맵 타입이어야 한다 (타입이 TypeName으로 주어질 때를 제외하고는 문법이 이러한 제약을 강요한다). 요소들과 키들의 타입은 리터럴 타입의 필드, 요소, 그리고 키 타입에 각각 [할당 가능해야](/Properties%20of%20types%20and%20values/assignability.html)하며; 추가적인 변환은 없다. 키는 구조체 리터럴에 대한 필드명으로, 배열과 슬라이스 리터럴의 인덱스로, 그리고 맵 리터럴의 키로 해석된다. 맵 리터럴에 대해서는, 모든 요소들이 키를 가져야 한다. 복수의 요소들이 같은 필드명이나 상수 키값을 지정하면 에러가 난다. 상수가 아닌 맵의 키들에 대해서는, [평가 순서](/Expressions/order_of_evaluation.html)를 참조하라.

구조체 리터럴은 다음의 규칙을 따른다:

  * 키는 struct 타입내 선언된 필드 이름이어야 한다.
  * 키를 포함하지 않은 요소는 필드가 선언된 순서대로 각 struct 필드에 대해 요소를 나열해야 한다.
  * 만약 단 하나의 요소라도 키를 가지고 있으면, 모든 요소에 키가 있어야 한다.
  * 키를 포함하는 요소들의 리스트가 각 struct 필드에 대한 요소를 반드시 가질 필요는 없다. 생략된 필드들은 해당 필드에 대해 제로값을 얻는다.
  * 요소 리스트가 생략되는 리터럴이 있을 수 있다; 그런 리터럴은 그 타입에 대한 제로값으로 평가된다.
  * 다른 패키지에 속한 struct의 엑스포트되지 않은 필드에 대해 요소를 지정하면 에러가 발생한다.

주어진 선언에 대해

```go
type Point3D struct { x, y, z float64 }
type Line struct { p, q Point3D }
```

다음과 같이 기술할 수 있다.

```go
origin := Point3D{}                            // Point3D에 제로값
line := Line{origin, Point3D{y: -4, z: 12.3}}  // line.q.x에 제로값
```

배열과 슬라이스 리터럴은 다음의 규칙을 따른다.

  * 각 요소들은 배열내 위치를 표시하는 연관된 정수 인덱스를 가진다.
  * 키를 가지는 요소는 키를 인덱스로 사용한다. 키는 `int` 타입의 값으로 나타낼 수 있는 음수가 아닌 상수여야 한다; 만약 타입이 있다면 정수 타입이어야 한다.
  * 키가 없는 요소는 바로 이전 요소의 인덱스에 1을 더한다. 만약 첫번째 요소가 키가 없으면, 그 인덱스는 0이다.

합성 리터럴의 [주소를 취하게 되면](/Expressions/address_operators.html) 리터럴의 값으로 초기화되는 독특한 [변수](/Variables/)를 가리키는 포인터가 생성된다.

```go
var pointer *Point3D = &Point3D{y: 1000}
```

배열 리터럴의 길이는 리터럴 타입내 지정된 길이이다. 만약 길이보다 적은 요소를 리터럴에 제공한 경우, 없는 요소에는 배열 요소 타입에 해당하는 제로값이 주어진다. 배열의 인덱스 범위밖의 인덱스 값들로 요소를 제공하면 에러가 난다. `...` 표시법은 최대 요소 인덱스에 하나를 더한 값과 같은 배열 길이를 지정한다.

```go
buffer := [10]string{}             // len(buffer) == 10
intSet := [6]int{1, 2, 3, 5}       // len(intSet) == 6
days := [...]string{"Sat", "Sun"}  // len(days) == 2
```

슬라이스 리터럴은 내재 배열 리터럴 전체를 나타낸다. 그러므로, 슬라이스의 길이와 용량은 최대 요소 인덱스 더하기 하나가 된다. 슬라이스 리터럴은 다음과 같은 형태이며

```go
[]T{x1, x2, … xn}
```

배열에 적용된 슬라이스 연산에 대한 속기이다.

```go
tmp := [n]T{x1, x2, … xn}
tmp[0 : n]
```

배열, 슬라이스, 혹은 맵 타입 `T`의 합성 리터럴안에서, 만약 `T`의 요소나 키 타입과 동일하다면 그 자체가 합성 리터럴인 요소나 맵의 키들은 각자에 해당하는 리터럴 타입을 생략해도 된다. 유사하게, 합성 리터럴의 주소인 요소나 키는 요소나 키의 타입이 `*T`일 때 `&T`를 생략할 수 있다.  

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

LiteralType의 TypeName 형태를 사용하는 합성 리터럴이 [키워드](/Lexical%20elements/keywords.html)와 "if", "for", 혹은 "switch" 구문 블록을 시작하는 중괄호 사이의 피연산자로 나타나고 합성 리터럴이 괄호, 각괄호, 혹은 중괄호안에 없는 경우 모호한 파싱이 일어날 수 있다. 이러한 드문 경우에, 시작하는 중괄호가 구문 블록을 도입하는 것으로 잘못 파싱된다. 리터럴의 이러한 모호함을 해결하기 위해, 합성 리터럴은 반드시 괄호안에 나타나야 한다.

```go
if x == (T{a,b,c}[i]) { … }
if (x == T{a,b,c}[i]) { … }
```

유효한 배열, 슬라이스, 그리고 맵 리터럴의 예제들:

```go
// 소수의 리스트
primes := []int{2, 3, 5, 7, 9, 2147483647}

// ch가 모음이면 vowels[ch] 는 true
vowels := [128]bool{'a': true, 'e': true, 'i': true, 'o': true, 'u': true, 'y': true}

// 배열 [10]float32{-1, 0, 0, 0, -0.1, -0.1, 0, 0, 0, -1}
filter := [10]float32{-1, 4: -0.1, -0.1, 9: -1}

// 균등한 스케일 (A4 = 440Hz)에 대해 주파수를 Hz로 표시
noteFrequency := map[string]float32{
    "C0": 16.35, "D0": 18.35, "E0": 20.60, "F0": 21.83,
    "G0": 24.50, "A0": 27.50, "B0": 30.87,
}
```
