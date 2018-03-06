# [한정적 식별자](#qualified-identifiers)

한정적 식별자는 패키지 이름을 접두사로 가지는 식별자다. 패키지 이름과 식별자는 [blank 식별자](/Declarations%20and%20scope/blank_identifier.html)가 아니여야 한다.

<pre>
<a id="QualifiedIdent">QualifiedIdent</a> = <a href="/Packages/package_clause.html#PackageName">PackageName</a> "." <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
</pre>

한정적 식별자는 [임포트 된](/Packages/import_declarations.html) 패키지의 식별자에 접근할 수 있다. 식별자는 반드시 [엑스포트 되어야](/Declarations%20and%20scope/exported_identifiers.html)하고, 그 패키지의 [패키지 블록](/Blocks/)안에서 선언해야 한다. 

```go
math.Sin    // 패키지 math내 Sin 함수를 나타낸다.
```
