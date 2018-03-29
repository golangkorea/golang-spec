# [소스 파일 구성](#source-file-organization)

각 소스 파일은 소속된 패키지를 정의하는 패키지 절과, 이어서 없을 수도 있는 임포트 선언이 따라오면서 사용하고자 하는 패키지를 선언하고, 부재가 허용되는 함수, 타입, 변수, 그리고 상수의 선언문 들이 따른다.

<pre>
<a id="SourceFile">SourceFile</a>       = <a href="/Packages/package_clause.html#PackageClause">PackageClause</a> ";" { <a href="/Packages/import_declarations.html#ImportDecl">ImportDecl</a> ";" } { <a href="/Declarations and scope/#TopLevelDecl">TopLevelDecl</a> ";" } .
</pre>
