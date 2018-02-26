# [한정적 식별자](#qualified-identifiers)

한정적 식별자는 패키지 이름을 접두사로 가지는 한정된 식별자이다. 패키지 이름과 식별자 둘 다 [blank](/Declarations%20and%20scope/blank_identifier.html)일 수 없다.

<pre>
<a id="QualifiedIdent">QualifiedIdent</a> = <a href="/Packages/package_clause.html#PackageName">PackageName</a> "." <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
</pre>

한정적 식별자는 다른 패키지의 식별자에 접근할 수 있으며, 이 패키지는 반드시 [임포트 되어야](/Packages/import_declarations.html)한다. 식별자는 반드시 [엑스포트 되어야](/Declarations%20and%20scope/exported_identifiers.html)하고, 그 패키지의 [패키지 블록](/Blocks/)안에 선언되어야 한다. 

```go
math.Sin    // 패키지 math내 Sin 함수를 나타낸다.
```
