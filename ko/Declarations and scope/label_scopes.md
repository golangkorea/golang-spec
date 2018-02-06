# [라벨 범위](#label-scopes)

라벨은 [라벨 문](https://golang.org/ref/spec#Labeled_statements)을 이용해 선언하고, "[break](https://golang.org/ref/spec#Break_statements)", "[continue](https://golang.org/ref/spec#Continue_statements)", "[goto](https://golang.org/ref/spec#Goto_statements)" 구문에서 사용된다. Go 문법은 라벨을 정의한 후 사용하지 않는 것은 허용하지 않는다. 다른 식별자들과는 대조적으로, 라벨은 블록 범위가 아니고, 라벨이 아닌 다른 식별자와 충돌하지 않는다. 라벨의 범위는 라벨을 선언한 함수의 본문이며, 중첩된 함수의 본문은 범위에서 제외된다.
