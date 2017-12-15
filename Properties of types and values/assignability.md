# [할당 가능한 값의 조건들(Assignability)](#assignability)

* Go 버전: 1.9
* 원문: [Assignability](https://golang.org/ref/spec#Assignability)
* 번역자: Jhonghee Park (@jhonghee)

A value x is assignable to a [variable](/Variables/) of type T ("x is assignable to T") in any of these cases:

  * x's type is identical to T.
  * x's type V and T have identical [underlying types](/Types/) and at least one of V or T is not a [defined](/Type_definitions/) type.
  * T is an interface type and x [implements](/Types/interface_types.html) T.
  * x is a bidirectional channel value, T is a channel type, x's type V and T have identical element types, and at least one of V or T is not a defined type.
  * x is the predeclared identifier nil and T is a pointer, function, slice, map, channel, or interface type.
  * x is an untyped [constant](/Constants/) representable by a value of type T.

어떤 값 x는 타입 T의 [변수](/Variables/)에 다음과 같은 조건일 경우 할당 가능하다(x는 T에 할당할 수 있다):

 * x의 타입이 T와 동일하다.
 * x의 타입 V와 T가 동일한 [내재 타입(underlying types)](/Types/)를 가지고 V와 T중에 적어도 하나는 [정의된(defined)](/Declarations%20and%20scope/type_declarations.html#type-definitions) 타입이 아니다.
 * T가 인터페이스 타입이고 x가 T를 [구현한다(implements)](/Types/interface_types.html).
 * x가 양방향 채널 값이고, T가 채널 타입일때, x의 타입 V와 T가 동일한 요소 타입을 가지고 있고, 적어도 V와 T중 하나는 정의된 타입이 아니다.
 * x가 미리 선언된 식별자인 nil이고 T가 포인터(pointer), 함수(function), 슬라이스(slice), 맵(map), 채널(channel), 그리고 인터페이스 타입이다.
 * x는 타입 T의 값으로 나타낼 수 있는 타입이 주어지지 않은 [상수(constant)](/Constants/) 값이다.