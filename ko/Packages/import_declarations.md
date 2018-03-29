# [임포트 선언](#import-declarations)

임포트 선언이 말하고 있는 바는  선언을 포함하고 있는 소스 파일이 *임포트된* 패키지 ([§프로그램 초기화와 실행](/Program%20initialization%20and%20execution/))의 기능에 의존하며 그 패키지의 [엑스포트 된](/Declarations%20and%20scope/exported_identifiers.html) 식별자들에 접근이 가능하다는 것이다. 임포트는 접근에 사용되는 식별자 (PackageName)와 임포트 되는 패키지를 명시하는 ImportPath에 이름을 제공한다.

<pre>
<a id="ImportDecl">ImportDecl</a>       = "import" ( <a href="#ImportSpec">ImportSpec</a> | "(" { <a href="#ImportSpec">ImportSpec</a> ";" } ")" ) .
<a id="ImportSpec">ImportSpec</a>       = [ "." | <a href="/Packages/package_clause.html#PackageName">PackageName</a> ] <a href="#ImportPath">ImportPath</a> .
<a id="ImportPath">ImportPath</a>       = <a href="/Lexical elements/string_literals.html#string_lit">string_lit</a> .
</pre>

PackageName은 [한정적 식별자](/Expressions/qualified_identifiers.html)속에 사용되어서 임포트를 하는 소스 파일안에 있는 패키지의 엑스포트된 식별자들을 접근하는데 쓰인다. 이 것은 [파일 블록](/Blocks/)안에 선언되어 있다. 만약 PackageName이 생략되면, [패키지 절](/Packages/package_clause.html)안에 명시된 식별자로 자동설정된다. 만약 이름 대신 명시적으로 마침표 (.)가 나타나면, 그 패키지의 [패키지 블록](/Blocks/)안에 선언된 모든 엑스포트된 식별자들이 임포트를 하는 소스 파일의 파일 블록안에 선언될 것이고 한정하는 식별자없이도 접근이 가능해야 한다.

ImportPath에 대한 해석은 구현마다 다를 수 있지만 보통은 컴파일된 패키지의 전체 파일 이름의 부분으로 구성되 문자열이고 설치된 패키지들의 레포지토리와 관련이 있을 수도 있다.

구현시 제약: 컴파일러는 ImportPath들에 대해 [유니코드](http://www.unicode.org/versions/Unicode6.3.0/)의 L, M, N, P,  그리고 S 일반 카테고리 (스페이스없는 그래픽 문자들)에 속한 문자들만 구성된 비어 있지 않은 문자열로 제한하거나 <code>!"#$%&'()*,:;<=>?[\]^`{|}</code>와 같은 문자들 그리고 유니코드 대체 문자인 U+FFFD을 제외할 수도 있다.

`Sin` 함수를 엑스포트하는, 패키지 절 `package math`를 포함하는 패키지를 컴파일하고 이 컴파일된 패키지를 `"lib/math"`로 식별되는 파일안에 설치하였다고 가정해 보라. 다음의 테이블은 임포트 선언의 여러 타입들에 따라서 그 패키지를 임포트하는 파일안에서 어떻게 `Sin`을 접근할 수 있는지 묘사하고 있다.

```go
임포트 선언          Sin의 로컬 이름

import   "lib/math"         math.Sin
import m "lib/math"         m.Sin
import . "lib/math"         Sin
```

하나의 임포트 선언은 임포트 하는 행위와 임포트된 패키지 사이에 있는 의존적인 관계를 선언한다. 직접적이든 간접적이든 패키지가 자체를 임포트하는 것은 허용되지 않고, 엑스포트되는 식별자들에 대한 참조하지 않으면서 패키지를 직접적으로 임포트하는 것도 허용되지 않는다. (초기화와 같은) 부작용만을 야기할 목적으로 패키지를 임포트 하고자 하면, [blank](/Declarations%20and%20scope/blank_identifier.html) 식별자를 명시적으로 패키지의 이름으로 사용하라:

```go
import _ "lib/math"
```
