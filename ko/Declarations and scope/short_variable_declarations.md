# [축약형 변수 선언](#short-variable-declarations)

*축약형 변수 선언*의 문법은 다음과 같다:

<pre>
<a id="ShortVarDecl">ShortVarDecl</a> = <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ":=" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> .
</pre>

축약형 변수 선언은 초기화 식은 있지만 타입은 명시되지 않은 일반적인 [변수 선언](/Declarations%20and%20scope/variable_declarations.html)의 축약 형태다.

```go
"var" IdentifierList = ExpressionList .
```

```go
i, j := 0, 10
f := func() int { return 7 }
ch := make(chan int)
r, w := os.Pipe(fd)  // os.Pipe()는 두 개의 값은 반환한다.
_, y, _ := coord(p)  // coord()는 세 개의 값은 반환한다; 관심있는 것은 y 좌표 하나 뿐임
```


정식 변수 선언문과는 달리, 축약형 변수 선언문은 같은 블록(블록이 함수 본문인 경우는 매개 변수 리스트) 안에서 이미 선언한 변수를 같은 타입으로 *재선언* 할 수 있는데, 이때 [blank](/Declarations%20and%20scope/blank_identifier.html) 식별자가 아닌 변수들 중 하나는 반드시 새로운 변수여야 한다. 즉, 재선언은 다중 변수에 대한 축약형 선언문에서만 가능하다. 재선언은 새로운 변수를 추가하는 것이 아니라 새로운 값을 원래 변수에 할당하는 것을 의미한다.

```go
field1, offset := nextField(str, 0)
field2, offset := nextField(str, offset)  // offset을 재선언한다.
a, a := 1, 2                              // 허용되지 않음: a에 대한 중복 선언 또는 a가 다른 곳에서 선언되어 있다면 새로운 변수가 없음.
```

축약형 변수 선언문은 함수 안에서만 사용할 수 있다. 추가적으로, "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", "[switch](/Statements/switch_statements.html)" 문에서 초기화 용도로 임시 로컬 변수를 선언하기 위해 사용하는 경우도 있다.


