# [패키지 절](#package-clause)

각 소스 파일은 이들이 속한 패키지를 정의하는 패키지 절로 시작한다.

<pre>
<a id="PackageClause">PackageClause</a>  = "package" <a href="#PackageName">PackageName</a> .
<a id="PackageName">PackageName</a>    = <a href="/Lexical elements/identifiers.html#identifier">identifier</a> .
</pre>

[blank 식별자](/Declarations%20and%20scope/blank_identifier.html)는 PackageName으로 사용할 수 없다.

```go
package math
```

같은 PackageName을 사용하는 파일들이 모여 하나의 패키지가 구현된다. 구현을 위해 패키지의 모든 소스 파일이 같은 디렉토리안에 있어야 하는 경우도 있다.
