# [For 문](#for-statements)

"for" 문은 블록의 반복적인 실행을 지정한다. 여기에는 단일 조건, "for" 문, 혹은 "range" 문을 통해 제어되는 세 가지의 형태가 있다.

<pre>
<a id="ForStmt">ForStmt</a> = "for" [ <a href="#Condition">Condition</a> | <a href="#ForClause">ForClause</a> | <a href="#RangeClause">RangeClause</a> ] <a href="/Blocks/#Block">Block</a> .
<a id="Condition">Condition</a> = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

## [단일 조건을 사용하는 For 문](#for-statements-with-single-condition)

단순한 형태에서, "for" 구문은 불린 조건이 `true`로 평가되는 동안에 해당 블록의 반복적인 실행을 지정한다. 이 조건은 각 이터레이션 직전에 평가된다. 조건이 없다면 항상 불린 값 `true`로 평가된다.

```go
for a < b {
    a *= 2
}
```

## [`for` 절을 사용하는 For 문](#for-statements-with-for-clause)

ForClause를 사용하는 "for" 문 또한 주어진 조건에 의해 제어되지만, 추가적으로 할당, 증가, 감소 명령과 같은 *init*과 *post* 문을 지정할 수 있다. init 문은 [짧은 변수 선언](/Declarations%20and%20scope/short_variable_declarations.html)일 수 있지만, post 문은 그래선 안된다. init 문을 통해 선언되는 변수들은 각 반복에서 재사용될 수 있다.

<pre>
<a id="ForClause">ForClause</a> = [ <a href="#InitStmt">InitStmt</a> ] ";" [ <a href="#Condition">Condition</a> ] ";" [ <a href="#PostStmt">PostStmt</a> ] .
<a id="InitStmt">InitStmt</a> = <a href="/Statements/#SimpleStmt">SimpleStmt</a> .
<a id="PostStmt">PostStmt</a> = <a href="/Statements/#SimpleStmt">SimpleStmt</a> .
</pre>

```go
for i := 0; i < 10; i++ {
    f(i)
}
```

비어있지 않다면, init 문은 첫번째 반복에 대한 조건을 평가하기 전에 한번만 실행된다; post 문은 블록의 실행 뒤에(블록이 실행된 경우에만) 매번 실행된다. ForClause의 모든 요소들은 비어있을 수도 있지만 조건만 있는 경우가 아닌 한에는 [세미콜론들](/Lexical%20elements/semicolons.html)이 필요하다. 조건이 없다면, 불린 값 `true`와 동일하다.

```go
for cond { S() }    는 다음과 동일    for ; cond ; { S() }
for      { S() }    는 다음과 동일    for true     { S() }
```

## [`range` 절을 사용하는 For 문](#for-statements-with-range-clause)

"range" 절을 사용하는 "for" 문은 배열, 슬라이스, 문자열 혹은 맵, 혹은 채널을 통해서 넘겨 받은 값들의 모든 요소들을 순회한다. 이 구문에서는 각 요소들에 대해 *반복 값*들을 이에 대응되는 *반복 변수*들에 할당한 다음 해당되는 블록을 실행한다.

<pre>
<a id="RangeClause">RangeClause</a> = [ <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> "=" | <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ":=" ] "range" <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

"range" 절의 우측에 있는 표현식은 *범위 표현식*이라고 불리며, 배열, 배열을 가리키는 포인터, 슬라이스, 문자열, 맵, 혹은 [수신 명령](/Expressions/receive_operator.html)을 허용하는 채널일 수 있다. 할당과 마찬가지로, 좌측에 피연산자가 있다면 이는 반드시 [주소 지정 가능](/Expressions/address_operators.html)하거나 맵 인덱스 표현식이어야 한다; 이러한 것들은  반복 변수들을 나타낸다. 범위 표현식이 채널이라면, 최대 하나의 반복 변수가 허용되며, 그렇지 않은 경우에는 둘 이상일 것이다. 마지막 반복 변수가 [공백 식별자](/Declarations%20and%20scope/blank_identifier.html)라면, range 절은 해당되는 식별자가 없는 것과 동일하다.

범위 표현식 `x`는 하나의 예외를 빼고는 이 루프가 시작되기 전에 한번만 평가된다: 범위 표현식이 배열이거나 배열을 가리키는 포인터이고, 최대 하나의 반복 변수가 존재한다면, 범위 표현식의 길이만이 평가된다; 이 길이가 상수라면, [그 정의에 의해](/Built-in%20functions/length_and_capacity.html) 범위 표현식 자신은 평가되지 않을 것이다.

좌측에서의 함수 호출은 매 반복 때마다 평가된다. 각 반복에 대한 반복 값들은 각 반복 변수가 존재하는 경우에 대해 다음과 같이 생성된다. 

<pre>
범위 표현식                          첫번째 값        두번째 값
&nbsp;
배열 혹은 슬라이스  a  [n]E, *[n]E, or []E    인덱스    i  int    a[i]       E
문자열          s  string type            인덱스    i  int    아래를 참고  rune
맵             m  map[K]V                키      k  K      m[k]       V
채널         c  chan E, &lt;-chan E       요소  e  E
</pre>

  1. 배열, 배열을 가리키는 포인터 혹은 슬라이스 값인 `a`에 대해, 인덱스 반복 값들은 요소 인덱스 0에서 시작하여 증가하는 순서로 생성된다. 최대 하나의 반복 변수가 존재한다면, range 루프는 0부터 `len(a)-1`까지 증가하는 반복 변수들을 생성하게 되고 배열이나 슬라이스 자체에 대한 색인을 생성하지 않는다. `nil` 슬라이스에 대한 반복 횟수는 0이다.
  2. 문자열 값에 대해, "range" 절은 문자열의 바이트 인덱스 0에서부터 시작하여 유니코드 코드 포인트 단위로 반복한다. 연속적인 반복에서, 위 표에서 말하는 인덱스의 값은 문자열 내에서 UTF-8으로 인코딩된 연속적인 코드 포인트의 첫번째 바이트가 될 것이다. 그리고 `rune` 타입의 두번째 값은, 코드 포인트에 대응되는 값이 될 것이다. 반복이 유효하지 않은 UTF-8 스퀀스에 마주치면, 두번째 값은 유니코드 대체 문자인 `0xFFFD`가 될 것이고, 다음 반복은 문자열 내에서 단일 바이트만큼 이동할 것이다.
  3. 맵에 대한 반복 순서는 무작위이며 한 반복이 다음 반복과 동일하다고 보장되지 않는다.
반복 동안에 아직 순회하지 않은 맵 요소가 삭제되었다면, 이에 대응되는 반복 값은 생성되지 않을 것이다. 반복 동안에 맵 요소가 생성된다면, 이 요소는 반복 동안에 생성될 수도 있고, 그냥 지나칠 수도 있다. 생성된 각 요소에 대한 선택은 반복마다 다를 수 있다. `nil` 맵에 대한 반복 횟수는 0이다.
  4. 채널에 대해 생성되는 반복 값들은 채널이 [닫히기](/Built-inunctions/close.html) 전까지 그 채널에서 보내진 연속적인 값들이다. `nil` 채널에 대한 범위 표현식은 영원히 블록된다.

반복 값들은 [할당문](/Statements/assignments.html)과 마찬가지로 각 반복 변수에 할당된다.

반복 변수들은 [짧은 변수 선언](/Declarations%20and%20scope/short_variable_declarations.html) (`:=`)의  형태를 사용하는 "range" 절을 통해 선언될 수도 있다. 이 경우, 반복 변수들의 타입은 각 반복 값들의 타입으로 정해지고 그 [스코프](/Declarationsndcope/)는 "for" 문의 블록이다; 반복 변수들은 각 반복 내에서 재사용될 수 있다. 반복 변수들이 "for"문의 바깥 쪽에서 선언되었다면, 이 변수들의 값은 마지막 반복이 실행된 후의 값이 될 것이다.

```go
var testdata *struct {
    a *[7]int
}
for i, _ := range testdata.a {
    // testdata.a는 절대 평가되지 않는다; len(testdata.a)는 상수
    // i의 범위는 0부터 6까지
    f(i)
}

var a [10]string
for i, s := range a {
    // i의 타입은 int
    // s의 타입은 string
    // s == a[i]
    g(i, s)
}

var key string
var val interface {}  // m의 값 타입은 val에 할당 가능
m := map[string]int{"mon":0, "tue":1, "wed":2, "thu":3, "fri":4, "sat":5, "sun":6}
for key, val = range m {
    h(key, val)
}
// key == 이터레이션 내에서 나타는 마지막 맵 키
// val == map[key]

var ch chan Work = producer()
for w := range ch {
    doWork(w)
}

// 빈 채널
for range ch {}
```