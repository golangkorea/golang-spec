# [할당문](#assignments)

<pre>
<a id="Assignment">Assignment</a> = <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> <a href="#assign_op">assign_op</a> <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> .
&nbsp;
<a id="assign_op">assign_op</a> = [ <a href="/Expressions/operators.html#add_op">add_op</a> | <a href="/Expressions/operators.html#mul_op">mul_op</a> ] "=" .
</pre>

[주소를 취할 수 있는](/Expressions/address_operators.html) 피연산자, 맵의 인덱스 식, 혹은 (`=` 할당에 한해서) [blank 식별자](/Declarations%20and%20scope/blank_identifier.html)만이 할당문의 왼쪽에 사용될 수 있다. 피연산자에는 괄호를 사용할 수 있다.

```go
x = 1
*p = f()
a[i] = 23
(k) = <-ch  // k = <-ch 와 같음
```

*op*가 이항 [산술 연산](/Expressions/arithmetic_operators.html)인 경우, 할당 연산인 `x` *op*`=` `y`는 `x` `=` `x` *op* `(y)`와 동등한 연산이지만 `x`는 한번만 평가된다. *op*`=` 성분은 단일 토큰이다. 할당 연산내, 왼쪽, 오른쪽 식들은 정확히 하나의 값을 산출하는 식이여야 하고, 왼쪽 식에 blank 식별자는 허용되지 않는다.

```go
a[i] <<= 2
i &^= 1<<n
```

튜플 할당문은 다중-값 연산의 각 요소를 변수 목록에 할당하는데 두 가지의 형식이 있다. 첫째로 오른쪽 피연산자가 함수 호출, [채널](/Types/channel_types.html), 또는 [맵](/Types/map_types.html) 연산, 혹은 [타입 단언](/Expressions/type_assertions.html)과 같은 단일 다중-값 식인 경우이다. 왼쪽에 있는 피연산자의 수는 이 값들의 수와 같아야 한다. 예를 들어, `f`가 두개의 값을 반환하는 함수인 경우,

```go
x, y = f()
```

위의 할당문은 첫번째 값이 `x`에 그리고 두번째 값이 `y`에 할당된다. 두번째 형식으로, 왼쪽의 피연산자 수가 오른쪽의 식의 수와 같은 경우로, 이 식들은 단일-값을 산출해야 하고 오른쪽의 *n*번째 식은 왼쪽의 *n*번째 피연산자에 할당된다:

```go
one, two, three = '一', '二', '三'
```

[blank 식별자](/Declarations%20and%20scope/blank_identifier.html)는 할당문에서 오른쪽 값들을 무시하는 방법을 제공한다:

```go
_ = x       // x를 평가하지만 무시한다
x, _ = f()  // f()를 평가하지만 두번째 반환값을 무시한다```

할당문은 두 단계로 전개된다. 첫째로, 왼쪽에 있는 [인덱스 식](/Expressions/index_expressions.html)의 피연산자와 ([선택자](/Expressions/selectors.html)내 함축된 포인터 간접 참조를 포함한) [포인터 간접 참조](/Expressions/address_operators.html)와 오른쪽에 있는 식들은 모두 [보통의 평가 순서](/Expressions/order_of_evaluation.html)를 따른다. 두번째로, 할당은 왼쪽에서 오른쪽으로 수행된다.

```go
a, b = b, a  // a와 b를 교환한다

x := []int{1, 2, 3}
i := 0
i, x[i] = 1, 2  // i = 1, x[0] = 2 로 설정한다

i = 0
x[i], i = 2, 1  // x[0] = 2, i = 1 로 설정한다

x[0], x[0] = 1, 2  // x[0] = 1 로 설정한 다음  x[0] = 2 로 다시 설정한다.   (결국 x[0] == 2 에 도달한다)

x[1], x[3] = 4, 5  // x[1] = 4 로 설정한 다음 x[3] = 5 를 설정할 때 패닉한다.

type Point struct { x, y int }
var p *Point
x[2], p.x = 6, 7  // x[2] = 6 로 설정한 다음 p.x = 7 를 설정할 때 패닉한다.

i = 2
x = []int{3, 5, 7}
for i, x[i] = range x {  // i, x[2] = 0, x[0] 로 설정한다
    break
}
// 이 루프가 끝나면, i == 0 이고 x == []int{3, 5, 3} 이다.
```

할당문내, 각 값은 할당하려고 하는 대상인 피연산자의 타입에 [할당 가능](/Propertiesf%20typesnd%20values/assignability.html)해야 하며, 다음과 같은 특수한 경우들이 있다:

  1. blank 식별자에는 어떤 타입의 값이든 할당할 수 있다.
  2. 인터페이스 타입의 변수나 blank 식별자에 미지정 타입의 상수가 할당되는 경우, 이 상수는 우선 자체의 [기본 타입](/Constants/)으로 [변환](/Expressions/conversions.html)된다.
  3. 인터페이스 타입의 변수나 blank 식별자에 미지정 타입의 불리언 값이 할당되는 경우, 이 값은 우선 `bool` 타입으로 변환된다.
