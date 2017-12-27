# [논리적 연산자(Logical operators)](#logical-operators)

* Go 버전: 1.9
* 원문: [Logical operators](https://golang.org/ref/spec#Logical_operators)
* 번역자: Jhonghee Park (@jhonghee)

Logical operators apply to [boolean](/Types/boolean_types.html) values and yield a result of the same type as the operands. The right operand is evaluated conditionally.

논리적 연산자들은 [불리언(boolean)](/Types/boolean_types.html) 값들에 적용되어 피연산자들과 같은 타입의 결괏값을 생산한다. 오른쪽 피연산자는 조건부로 평가된다.

```
&&    conditional AND    p && q  is  "if p then q else false"
||    conditional OR     p || q  is  "if p then true else q"
!     NOT                !p      is  "not p"
```

```
&&    조건적 AND    p && q  는  "p가 참이면 q값이 결괏값이고 그렇지 않으면 false"
||    조건적 OR     p || q  는  "p가 참이면 true 그렇지 않으면 q값이 결괏값"
!     NOT         !p      는  "p가 아닌 값"
```
