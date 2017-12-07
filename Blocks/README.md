# [블록(Blocks)](#blocks)

* Go 버전: 1.9
* 원문: [Blocks](https://golang.org/ref/spec#Blocks)
* 번역자: Jhonghee Park (@jhonghee)

A *block* is a possibly empty sequence of declarations and statements within matching brace brackets.

*블락*은 서로 짝이 맞는 브래이스 브래킷(brace brackets) 범위내의 순차적인 선언문들과 실행문들로 공백의 블락도 가능하다.

<pre>
<a id="Block">Block</a> = "{" <a href="#StatementList">StatementList</a> "}" .
<a id="StatementList">StatementList</a> = { <a href="/Statements/#Statement">Statement</a> ";" } .
</pre>

In addition to explicit blocks in the source code, there are implicit blocks:

  1. The *universe block* encompasses all Go source text.
  2. Each [package](/Packages/) has a *package block* containing all Go source text for that package.
  3. Each file has a *file block* containing all Go source text in that file.
  4. Each "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", and "[switch](/Statements/switch_statements.html)" statement is considered to be in its own implicit block.
  5. Each clause in a "[switch](/Statements/switch_statements.html)" or "[select](/Statements/select_statements.html)" statement acts as an implicit block.

소스 코드내에는 명시적인 블락과 더불어 함축적인 블락도 있다:

  1. *유니버스 블락(universe block)*은 Go 소스 텍스트 전체를 포함한다.
  2. 각 [패키지(package)](/Packages/)는 그 패키지에 속하는 모든 Go 소스 텍스트를 포함하는 *패키지 블락*이 있다.
  3. 각 파일에는 그 파일내 모든 Go 소스 텍스트를 포함하는 *파일 블락(file block)*이 있다.
  4. 각 "[if](/Statements/if_statements.html)", "[for](/Statements/for_statements.html)", 그리고 "[switch](/Statements/switch_statements.html)" 실행문은 그 자체의 함축적인 블락속에 있다고 볼 수 있다.
  5. 하나의 "[switch](/Statements/switch_statements.html)" 혹은 "[select](/Statements/select_statements.html)" 실행문내 각각의 절(clause)은 함축적인 블락으로 동작한다.

Blocks nest and influence scoping.

블락들은 네스팅을 하고 변수의 가시 범위를 결정하는데 영향을 미친다.