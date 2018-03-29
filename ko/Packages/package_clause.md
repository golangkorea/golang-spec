# [패키지 절](#package-clause)

각 소스 파일은 패키지 절을 통해 시작되고 파일이 속한 패키지를 정의한다.

<pre>
<a id="PackageClause">PackageClause</a>  = "package" <a href="#PackageName">PackageName</a> .
<a id="PackageName">PackageName</a>    = <a href="/Lexical elements/identifiers.html#identifier">identifier</a> .
</pre>

PackageName은 [blank 식별자](/Declarations%20and%20scope/blank_identifier.html)일 수 없다.

```go
package math
```

같은 PackageName을 공유하는 파일들은 한 패키지의 구현을 형성한다. 구현의 한 방식으로 패키지에 대한 모든 소스 파일이 같은 디렉토리안에 존재할 것을 요구할 수도 있다.
