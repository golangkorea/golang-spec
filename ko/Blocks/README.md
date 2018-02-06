# [블록](#blocks)

*블록*은 서로 짝이 맞는 브래이스 브래킷(brace brackets) 범위내의 순차적인 선언문들과 실행문들로 공백의 블록도 가능하다.

<pre>
<a id="Block">Block</a> = "{" <a href="#StatementList">StatementList</a> "}" .
<a id="StatementList">StatementList</a> = { <a href="/Statements/#Statement">Statement</a> ";" } .
</pre>

소스 코드내에는 명시적인 블록과 더불어 함축적인 블록도 있다:

  1. *유니버스 블록(universe block)*은 Go 소스 텍스트 전체를 포함한다.
  2. 각 [패키지(package)](/Packages/)는 그 패키지에 속하는 모든 Go 소스 텍스트를 포함하는 *패키지 블록*이 있다.
  3. 각 파일에는 그 파일내 모든 Go 소스 텍스트를 포함하는 *파일 블록(file block)*이 있다.
  4. 각 "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", 그리고 "[switch](/Statements/switch_statements.html)" 실행문은 그 자체의 함축적인 블록속에 있다고 볼 수 있다.
  5. 하나의 "[switch](/Statements/switch_statements.html)" 혹은 "[select](/Statements/select_statements.html)" 실행문내 각각의 절(clause)은 함축적인 블록으로 동작한다.

블록들은 네스팅을 하고 변수의 가시 범위를 결정하는데 영향을 미친다.
