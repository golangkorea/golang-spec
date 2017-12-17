# [구문(Statements)](#statements)

* Go 버전: 1.9
* 원문: [Statements](https://golang.org/ref/spec#Statements)
* 번역자: [조석규](@ezaurum)

Statements control execution.

구문은 실행을 관리한다.

<pre>
<a id="Statement">Statement</a> =
	<a href="/Declarations%20and%20scope/#Declaration">Declaration</a> | <a href="/Statements/labeled_statements.html#LabeledStmt">LabeledStmt</a> | <a href="#SimpleStmt">SimpleStmt</a> |
	<a href="/Statements/go_statements.html#GoStmt">GoStmt</a> | <a href="/Statements/return_statements.html#ReturnStmt">ReturnStmt</a> | <a href="/Statements/break_statements.html#BreakStmt">BreakStmt</a> | <a href="/Statements/continue_statements.html#ContinueStmt">ContinueStmt</a> | <a href="/Statements/goto_statements.html#GotoStmt">GotoStmt</a> |
	<a href="/Statements/fallthrough_statements.html#FallthroughStmt">FallthroughStmt</a> | <a href="/Blocks/#Block">Block</a> | <a href="/Statements/if_statements.html#IfStmt">IfStmt</a> | <a href="/Statements/switch_statements.html#SwitchStmt">SwitchStmt</a> | <a href="/Statements/select_statements.html#SelectStmt">SelectStmt</a> | <a href="/Statements/for_statements.html#ForStmt">ForStmt</a> |
	<a href="/Statements/defer_statements.html#DeferStmt">DeferStmt</a> .
&nbsp;
<a id="SimpleStmt">SimpleStmt</a> = <a href="/Statements/empty_statements.html#EmptyStmt">EmptyStmt</a> | <a href="/Statements/expression_statements.html#ExpressionStmt">ExpressionStmt</a> | <a href="/Statements/send_statements.html#SendStmt">SendStmt</a> | <a href="/Statements/incdec_statements.html#IncDecStmt">IncDecStmt</a> | <a href="/Statements/assignments.html#Assignment">Assignment</a> | <a href="/Declarations%20and%20scope/short_variable_declarations.html#ShortVarDecl">ShortVarDecl</a> .
</pre>
