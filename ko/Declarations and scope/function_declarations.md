# [함수 선언문](#function-declarations)

함수 선언문은 식별자인 *함수 이름* 을 함수와 연결한다.

<pre>
<a id="FunctionDecl">FunctionDecl</a> = "func" <a href="#FunctionName">FunctionName</a> ( <a href="#Function">Function</a> | <a href="/Types/function_types.html#Signature">Signature</a> ) .
<a id="FunctionName">FunctionName</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
<a id="Function">Function</a>     = <a href="/Types/function_types.html#Signature">Signature</a> <a href="#FunctionBody">FunctionBody</a> .
<a id="FunctionBody">FunctionBody</a> = <a href="/Blocks/#Block">Block</a> .
</pre>

함수의 [시그니처](/Types/function_types.html)가 결과 매개 변수를 선언했다면, 함수 본문에 있는 구문 리스트는 반드시 [종결문](/Statements/terminating_statements.html)으로 끝나야 한다.

```go
func IndexRune(s string, r rune) int {
    for i, c := range s {
        if c == r {
            return i
        }
    }
    // 유효하지 않음: 리턴 구문이 없음
}
```

함수 선언시 본문을 생략할 수도 있다. 이런 선언문은 어셈블리 루틴와 같은 Go 외부에서 구현된 함수에 대한 시그니처를 제공한다.

```go
func min(x int, y int) int {
    if x < y {
        return x
    }
    return y
}

func flushICache(begin, end uintptr)  // 외부에서 구현됨
```
