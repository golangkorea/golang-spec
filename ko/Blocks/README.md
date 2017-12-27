# [블록](#blocks)

*블록*은 서로 짝이 맞는 브래이스 브래킷(brace brackets) 범위내의 순차적인 선언문들과 실행문들로 공백의 블록도 가능하다.

<pre>
<a id="Block">Block</a> = "{" <a href="#StatementList">StatementList</a> "}" .
<a id="StatementList">StatementList</a> = { <a href="/Statements/#Statement">Statement</a> ";" } .
</pre>

소스 코드내에는 명시적인 블록과 더불어 함축적인 블록도 있다:

1. *유니버스 블록(universe block)*은 Go 소스 텍스트 전체를 포함한다.
2. 각 [ 패키지(package)](/Packages/)는 그 패키지에 속하는 모든 Go 소스 텍스트를 포함하는 *패키지 블록*이 있다.
3. 각 파일에는 그 파일내 모든 Go 소스 텍스트를 포함하는 *파일 블록(file block)*이 있다.
4. Each "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", and "[switch](/Statements/switch_statements.html)" statement is considered to be in its own implicit block.
5. Each clause in a "[switch](/Statements/switch_statements.html)" or "[select](/Statements/select_statements.html)" statement acts as an implicit block.

Blocks nest and influence scoping.