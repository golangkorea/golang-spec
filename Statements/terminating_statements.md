# [종결문(Terminating statements)](terminating-statements)

* Go 버전: 1.9
* 원문: [Terminating statements](https://golang.org/ref/spec#Terminating_statements)
* 번역자: [조석규](@ezaurum)

A terminating statement is one of the following:

종결문은 다음 중 하나이다.

  1. A "[return](/Statements/return_statements.html)" or "[goto](/Statements/goto_statements.html)" statement.
  2. A call to the built-in function [panic](/Built-in%20functions/handling_panics.html).
  3. A [block](/Blocks/#Block) in which the statement list ends in a terminating statement.
  4. An ["if" statement](/Statements/if_statements.html) in which:
    * the "else" branch is present, and
    * both branches are terminating statements.
  5. A ["for" statement](/Statements/for_statements.html) in which:
    * there are no "break" statements referring to the "for" statement, and
    * the loop condition is absent.
  6. A ["switch" statement](/Statements/switch_statements.html) in which:
    * there are no "break" statements referring to the "switch" statement,
    * there is a default case, and
    * the statement lists in each case, including the default, end in a terminating statement, or a possibly labeled ["fallthrough" statement](/Statements/fallthrough_statements.html).
  7. A ["select" statement](/Statements/select_statements.html) in which:
    * there are no "break" statements referring to the "select" statement, and
    * the statement lists in each case, including the default if present, end in a terminating statement.
  8. A [labeled statement](/Statements/labeled_statements.html) labeling a terminating statement.

  1. "[return](/Statements/return_statements.html)" 이나 "[goto](/Statements/goto_statements.html)" 문.
  2. 내장된 [panic](/Built-in%20functions/handling_panics.html) 함수 호출.
  3. 종결문으로 끝나는 [블록](/Blocks/#Block).
  4. ["if" 문](/Statements/if_statements.html)이 다음과 같을 때:
    * "else" 가지가 있고,
    * 양쪽 가지가 모두 종결문으로 끝난다.
  5. A ["for" 문](/Statements/for_statements.html) 이 다음과 같을 때:
    * "for" 문을 지칭하는 "break" 문이 없고,
    * 반복 조건이 없는 경우.
  6. A ["switch" 문](/Statements/switch_statements.html) 이 다음과 같을 때:
    * "switch" 문을 지칭하는 "break" 문이 없고,
    * default case가 있고,
    * default를 포함해서 각 case 의 문 목록이, 종결문으로 끝나거나 라벨이 ["fallthrough" 문](/Statements/fallthrough_statements.html) 인 경우.
  7. A ["select" 문](/Statements/select_statements.html) 이 다음과 같을 때:
    * "select" 문을 지칭하는 "break" 문이 없고,
    * default를 포함해서 각 case 의 문 목록이, 종결문으로 끝나는 경우.
  8. 종결문을 가리키는 [라벨 문](/Statements/labeled_statements.html).

All other statements are not terminating.

다른 문은 종결문이 아니다.

A [statement list](/Blocks/) ends in a terminating statement if the list is not empty and its final non-empty statement is terminating.

[문 목록](/Blocks/) 목록이 비지 않고, 마지막 비지 않은 문이 종결문이면 문을 종결한다.
