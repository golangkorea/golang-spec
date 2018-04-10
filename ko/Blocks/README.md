# [블록](#blocks)

선언문과 구문이 중괄호 안에 하나도 없거나 여러 개가 나열되어 있는 것을 *블록* 이라고 부른다.

<pre>
<a id="Block">Block</a> = "{" <a href="#StatementList">StatementList</a> "}" .
<a id="StatementList">StatementList</a> = { <a href="/Statements/#Statement">Statement</a> ";" } .
</pre>

소스 코드 안에는 명시적인 블록뿐만 아니라 함축적인 블록도 있다:

  1. *유니버스 블록(universe block)* 은 Go 소스 코드 전체를 의미한다.
  2. 각 [패키지(package)](/Packages/)에는 패키지에 속한 모든 Go 소스 코드를 포괄하는 *패키지 블록* 이 있다.
  3. 각 파일에는 파일에 있는 모든 Go 소스 코드가 포함된 *파일 블록(file block)* 이 있다.
  4. 각 "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", "[switch](/Statements/switch_statements.html)" 문은 그들만의 함축 블록이 있는 것으로 간주된다. 
  5. "[switch](/Statements/switch_statements.html)" 나 "[select](/Statements/select_statements.html)" 문의 각 절(clause)은 함축적인 블록처럼 동작한다.

블록은 중첩될 수 있으며 [범위](/Declarations%20and%20scope/)를 결정하는데 영향을 미친다.
