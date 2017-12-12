# [Label scopes(Label scopes)](#Label scopes)

* Go 버전: 1.9
* 원문: [Label scopes](https://golang.org/ref/spec#Label_scopes)
* 번역자: Minseok Han (@mitrilmad)

Labels are declared by [labeled statements](https://golang.org/ref/spec#Labeled_statements) and are used in the "[break](https://golang.org/ref/spec#Break_statements)", "[continue](https://golang.org/ref/spec#Continue_statements)", and "[goto](https://golang.org/ref/spec#Goto_statements)" statements. It is illegal to define a label that is never used. In contrast to other identifiers, labels are not block scoped and do not conflict with identifiers that are not labels. The scope of a label is the body of the function in which it is declared and excludes the body of any nested function.

라벨은 [라벨 명령문](https://golang.org/ref/spec#Labeled_statements)에 의해 선언 되고, "[break](https://golang.org/ref/spec#Break_statements)", "[continue](https://golang.org/ref/spec#Continue_statements)", "[goto](https://golang.org/ref/spec#Goto_statements)" 명령문에서 사용 된다. 사용되지 않는 라벨을 정의 하는 것은 불법이다. 다른 식별자들과는 대조적으로, 라벨은 블록 범위가 아니고, 라벨이 아닌 다른 식별자와 충돌 하지 않는다. 라벨의 범위는 선언된 함수의 바디 내부 이고, 내장된 함수의 바디는  제외된다.
