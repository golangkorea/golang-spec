# [소스 파일 구성](#source-file-organization)

각 소스 파일은 자신이 소속된 패키지를 정의하는 패키지 절(clause), 사용하고 싶은 패키지를 선언하는 임포트 선언문(없는 경우도 있음), 함수, 타입, 변수, 상수에 대한 선언문(없는 경우도 있음) 순서로 구성된다.

<pre>
<a id="SourceFile">SourceFile</a>       = <a href="/Packages/package_clause.html#PackageClause">PackageClause</a> ";" { <a href="/Packages/import_declarations.html#ImportDecl">ImportDecl</a> ";" } { <a href="/Declarations and scope/#TopLevelDecl">TopLevelDecl</a> ";" } .
</pre>
