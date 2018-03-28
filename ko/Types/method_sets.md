# [메서드 집합](#method-sets)

타입은 관련 *메서드 집합(method set)* 을 가질 수 있다. [interface 타입](/Types/interface_types.html)의 메서드 집합은 인터페이스 그 자체다. 그밖의 타입 `T` 에 대한 메서드 집합은 모든 [메서드](/Declarations%20and%20scope/method_declarations.html)의 수신자(receiver)가 타입 `T` 로 선언되어 있다. [포인터 타입](/Types/pointer_types.html) `*T` 에 대응되는 메서드 집합은 수신자(receiver)가 `*T` 또는 `T`(즉, `T`의 메서드 집합 또한 포함된다.) 인 모든 메서드들의 집합이다. 임베디드 필드를 포함하고 있는 구조체에 대해 적용되는 추가적인 규칙은 [struct 타입](/Types/struct_types.html) 섹션에서 확인할 수 있다. 그밖의 타입은 빈 메서드 집합을 가진다. 메서드 집합 안에서 각 메서드는 [blank 식별자](/Declarations%20and%20scope/blank_identifier.html)가 아닌 [고유한](/Declarations%20and%20scope/uniqueness_of_identifiers.html) [메서드 이름](/Types/interface_types.html#MethodName)을 가져야 한다.

타입의 메서드 집합은 그 타입이 [구현(implements)](/Types/interface_types.html)하는 인터페이스와 그 타입의 수신자(receiver)를 사용하여 [호출](/Expressions/calls.html)될 수 있는 메서드를 결정한다.
