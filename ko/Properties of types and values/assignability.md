# [할당 가능한 값의 조건들](#assignability)

어떤 값 x는 타입 T의 [변수](/Variables/)에 다음과 같은 조건일 경우 할당 가능하다(x는 T에 할당할 수 있다):

  * x의 타입이 T와 동일하다.
  * x의 타입 V와 T가 동일한 [내재 타입(underlying types)](/Types/)를 가지고 V와 T중에 적어도 하나는 [정의된(defined)](/Declarations%20and%20scope/type_declarations.html#type-definitions) 타입이 아니다.
  * T가 인터페이스 타입이고 x가 T를 [구현한다(implements)](/Types/interface_types.html).
  * x가 양방향 채널 값이고, T가 채널 타입일때, x의 타입 V와 T가 동일한 요소 타입을 가지고 있고, 적어도 V와 T중 하나는 정의된 타입이 아니다.
  * x가 미리 선언된 식별자인 nil이고 T가 포인터(pointer), 함수(function), 슬라이스(slice), 맵(map), 채널(channel), 그리고 인터페이스 타입이다.
  * x는 타입 T의 값으로 나타낼 수 있는 타입이 주어지지 않은 [상수(constant)](/Constants/) 값이다.
