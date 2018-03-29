# [선언과 범위](#declarations_and_scope)

*선언*은 [blank](/Declarations%20and%20scope/blank_identifier.html)가 아닌 식별자를 [상수](/Declarations%20and%20scope/blank_identifier.html), [타입](/Declarations%20and%20scope/type_declarations.html), [변수](/Declarations%20and%20scope/variable_declarations.html), [함수](/Declarations%20and%20scope/function_declarations.html), [라벨](/Statements/labeled_statements.html), 혹은 [패키지](/Packages/import_declarations.html)에 바인딩한다. 프로그램내 모든 식별자는 선언되어야 한다. 동일한 블록안에서 같은 식별자를 두번이상 선언할 수 없고, 파일과 패키지 블록안에 동시에 선언될 수 없다.

[blank 식별자](/Declarations%20and%20scope/blank_identifier.html)는 다른 식별자와 마찬가지로 선언에 사용이 가능하지만, 바인딩이 생기지 않기 때문에 선언된 것은 아니다. 패키지 블록안에서, 식별자 `init`는 [init 함수](/Program%20initialization%20and%20execution/package_initialization.html)를 선언하는 데만 사용할 수 있고, blank 식별자와 마찬가지로 새로운 바인딩을 도입하지 않는다.

<pre>
<a id="Declaration">Declaration</a>   = <a href="/Declarations%20and%20scope/constant_declarations.html#ConstDecl">ConstDecl</a> | <a href="/Declarations%20and%20scope/type_declarations.html#TypeDecl">TypeDecl</a> | <a href="/Declarations%20and%20scope/variable_declarations.html#VarDecl">VarDecl</a> .
<a id="TopLevelDecl">TopLevelDecl</a>  = <a href="#Declaration">Declaration</a> | <a href="/Declarations%20and%20scope/function_declarations.html#FunctionDecl">FunctionDecl</a> | <a href="/Declarations%20and%20scope/method_declarations.html#MethodDecl">MethodDecl</a> .
</pre>

선언된 식별자의 *범위*는 그 식별자가 지정된 상수, 타입, 변수, 함수, 라벨 또는 패키지를 나타내는 소스 텍스트의 범위입니다.

Go는 [블록](/Blocks/)을 이용하여 어휘적 범위를 지정한다:

  1. [미리 선언된 식별자](/Declarations%20and%20scope/predeclared_identifiers.html)의 범위는 유니버스(universe) 블록이다.
  2. (함수의 외부이며) 최상위 레벨에서 선언된 상수, 타입, 변수, 혹은 (메서드는 제외한) 함수를 나타내는 식별자의 범위는 패키지 블록이다.
  3. 임포트된 패키지의 이름에 대한 범위는 임포트 선언문을 포함하고 있는 파일의 블록이다.
  4. 메서드 리시버, 함수 매개변수, 또는 결과 변수를 나타내는 식별자의 범위는 함수의 본문이다.
  5. 함수 안에 선언된 상수 혹은 변수 식별자의 범위는 ConstSpec 혹은 VarSpec (짧은 변수 선언문의 경우는 ShortVarDecl)가 끝나자 마자 시작해서 이들이 포함된 블록들중 가장 깊은 것의 끝에서 끝난다.
  6. 함수 안에 선언된 타입 식별자의 범위는 TypeSpec내 식별자에서 시작해서 이들이 포함된 블록들중 가장 깊은 것의 끝에서 끝난다.

한 블록에서 선언된 식별자는 더 깊은 내부 블록에서 재선언될 수 있다. 더 깊은 내부에서 선언된 식별자는 범위안에 있는 동안에는 내부 선언문에 의해 선언된 것을 나타낸다.

[패키지 절](/Packages/package_clause.html)은 선언문이 아니다; 패키지 이름은 어느 범위에도 나타나지 않는다. 이 것의 목적은 같은 [패키지](/Packages/)에 속하는 파일들을 확인하고 임포트 선언문에 사용되는 디폴트 패키지 이름을 지정하기 위한 것이다.
