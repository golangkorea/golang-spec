# [짧은 변수 선언](#short-variable-declarations)

*짧은 변수 선언*의 문법은 다음과 같다:

<pre>
<a id="ShortVarDecl">ShortVarDecl</a> = <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ":=" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> .
</pre>

초기값이 있는 정식 [변수 선언](/Declarations%20and%20scope/variable_declarations.html)를 짧게 한 것이며 타입이 없다:

```go
"var" IdentifierList = ExpressionList .
```

```go
i, j := 0, 10
f := func() int { return 7 }
ch := make(chan int)
r, w := os.Pipe(fd)  // os.Pipe()는 두개의 값은 반환한다.
_, y, _ := coord(p)  // coord()는 세개의 값은 반환한다; 오직 y 좌표만 원한다```

정식 변수 선언문과는 달리, 짧은 변수 선언문은 같은 블록안에서 이미 선언된 바 있는 변수를 (또한 블록이 함수 본문인 경우는 매개 변수 리스트를) 같은 타입을 사용해 *재선언*할 수 있는데, 이때 [blank](/Declarations%20and%20scope/blank_identifier.html)가 아닌 변수들 중 적어도 하나는 새로운 것이야 한다. 그 결과로, 재선언은 다중 변수의 짧은 선언문안에서만 일어 날 수 있다. 재선언은 새로운 변수를 도입하는 것이 아니라; 새로운 값을 원래 변수에 할당하는 것이다.

```go
field1, offset := nextField(str, 0)
field2, offset := nextField(str, offset)  // offset을 재선언한다.
a, a := 1, 2                              // 허용되지 않음: a를 반복 선언하거나 만약 a가 다른 곳에서 선언 되었다면 새로운 변수가 아니다.
```

짧은 변수 선언문은 함수 내부에서만 나타날 수 있다. 다만 "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", 혹은 "[switch](/Statements/switch_statements.html)" 구문을 위한 초기화로 쓰이는 상황에는, 임시적인 로컬 변수를 선언하는데 사용될 수도 있다. 


