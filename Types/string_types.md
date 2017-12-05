# String types

# [String 타입(String types)](#string-types)

* Go 버전: 1.9
* 원문 : [String types](https://golang.org/ref/spec#String_types)
* 번역자 : [연규민](@voidsatisfaction)

A *string type* represents the set of string values. A string value is a (possibly empty) sequence of bytes. Strings are immutable: once created, it is impossible to change the contents of a string. The predeclared string type is `string`.

*String 타입*은 String 값들의 집합을 나타낸다. 하나의 String 값은(비어있을 수 있음) 바이트들의 연속 이다. 모든 String은 불변이다: 한 번 생성된 String의 내용을 변경하는 것은 불가능하다. 미리 선언된 String의 타입은 `string`이다.

The length of a string s (its size in bytes) can be discovered using the built-in function [len](/Built-in%20functions/length_and_capacity.html). The length is a compile-time constant if the string is a constant. A string's bytes can be accessed by integer [indices](/Expressions/index_expressions.html) 0 through `len(s)-1`. It is illegal to take the address of such an element; if `s[i]` is the i'th byte of a string, `&s[i]` is invalid.

어떠한 String s의 길이(바이트 사이즈)는 내장함수인 [len](/Built-in%20functions/length_and_capacity.html)를 이용해서 구할 수 있다. 만약 String이 상수일 경우 그 길이는 컴파일시 계산된 상수 값이다. 한 String의 바이트는 0부터 `len(s)-1`까지의 정수 [인덱스들](/Expressions/index_expressions.html)로 접근 가능하다. 그러나 String의 요소 하나의 주소를 가져올 수 없다; 만약 `s[i]`이 어떠한 String의 i번째 바이트라면, `&s[i]`는 사용할 수 없다.
