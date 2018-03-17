# [select 문](#select-statements)

"select" 문은 가능한 [송신](/Statements/send_statements.html) 혹은 [수신](/Expressions/receive_operator.html) 연산들의 집합에서 어느 것으로 진행할 것인지를 선택한다. "[switch](/Statements/switch_statements.html)" 문과 유사하나 모든 케이스들이 통신 연산이라는 점이 다르다.

<pre>
<a id="SelectStmt">SelectStmt</a> = "select" "{" { <a href="#CommClause">CommClause</a> } "}" .
<a id="CommClause">CommClause</a> = <a href="#CommCase">CommCase</a> ":" <a href="/Blocks/#StatementList">StatementList</a> .
<a id="CommCase">CommCase</a>   = "case" ( <a href="/Statements/send_statements.html#SendStmt">SendStmt</a> | <a href="#RecvStmt">RecvStmt</a> ) | "default" .
<a id="RecvStmt">RecvStmt</a>   = [ <a href="/Blocks/#ExpressionList">ExpressionList</a> "=" | <a href="/Blocks/#IdentifierList">IdentifierList</a> ":=" ] <a href="#RecvExpr">RecvExpr</a> .
<a id="RecvExpr">RecvExpr</a>   = <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

RecvStmt가 사용된 케이스는 RecvExpr의 결괏값을 하나 혹은 두개의 변수에, [짧은 변수 선언](/Declarations%20and%20scope/short_variable_declarations.html)를 써서 할당할 수 있다. RecvExpr는 (괄호가 사용될 수 있는) 수신 연산이어야 한다. 적어도 하나의 기본 케이스가 존재해야 하며, 케이스 목록중에 아무데나 위치해도 상관없다.

"select" 문의 실행은 몇 단계를 거쳐 나아간다.

  1. 구문안의 모든 케이스에 대해, 수신 연산들의 채널 피연산자들과 송신 구문들의 오른쪽 식들과 채널은, "select" 문으로 들어가면서 소스에 나타난 순서대로, 정확히 한번씩만 평가된다. 그 결과는 수신과 송신을 하게 될 채널의 집합과 송신할 해당 값들을 얻는다. 이 평가 과정에서 전개될 통신 연산의 선택과 무관한 부작용이 일어날 수 있다. 짧은 변수 선언이나 할당를 가지고 있는 RecvStmt의 왼쪽에 있는 식들은 아직 평가되지 않았다.
  2. 하나 혹은 그 이상의 통신이 전개되는 경우는, 균일한 의사 랜덤 선택을 통해 선택된다. 그렇지 않은 경우라면, 기본 케이스가 있고, 그 것이 선택된 경우이다. 만약 기본 케이스가 없는 경우는, 나아갈 수 있는 통신이 적어도 하나 생길 때까지 "select" 문은 블록이 된다.
  3. 기본 케이스가 선택되지 않는 이상, 해당 통신 연산이 실행된다.
  4. 만약 선택된 케이스가 짧은 변수 선언 혹은 할당문이 있는 RecvStmt이면, 왼쪽 식은 평가되고 수신된 값(혹은 값들)은 할당된다.
  5. 선택된 케이스의 구문 목록이 실행된다.

`nil` 채널들에 대한 통신은 결코 진행될 수 없기 때문에, `nil` 채널들을 가지고 있는 케이스나 기본 케이스가 없을 때는 영원히 블록된다.

```go
var a []int
var c, c1, c2, c3, c4 chan int
var i1, i2 int
select {
case i1 = <-c1:
    print("received ", i1, " from c1\n")
case c2 <- i2:
    print("sent ", i2, " to c2\n")
case i3, ok := (<-c3):  // i3, ok := <-c3 와 같음
    if ok {
        print("received ", i3, " from c3\n")
    } else {
        print("c3 is closed\n")
    }
case a[f()] = <-c4:
    // 밑에 있는 케이스만과 같음:
    // case t := <-c4
    //  a[f()] = t
default:
    print("no communication\n")
}

for {  // 랜덤한 비트가 연속으로 c로 보내진다
    select {
    case c <- 0:  // 주의: 구문이 없고, fallthrough도 없고, 케이스들이 중단되지도 않는다
    case c <- 1:
    }
}

select {}  // 영원히 블록한다
```
