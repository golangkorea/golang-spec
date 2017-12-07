# [메서드 집합(Method sets)](#method-sets)

* Go 버전: 1.9
* 원문: [Method sets](https://golang.org/ref/spec#Method_sets)
* 번역자: 허성연 (@hursungyun)

A type may have a method set associated with it. The method set of an [interface type](/Types/interface_types.html) is its interface. The method set of any other type T consists of all [methods](/Declarations%20and%20scope/method_declarations.html) declared with receiver type T. The method set of the corresponding [pointer type](/Types/pointer_types.html) *T is the set of all methods declared with receiver *T or T (that is, it also contains the method set of T). Further rules apply to structs containing embedded fields, as described in the section on [struct types](/Types/struct_types.html). Any other type has an empty method set. In a method set, each method must have a [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html) non-[blank](/Declarations%20and%20scope/blank_identifier.html) [method name](/Types/interface_types.html#MethodName).

어떠한 타입은 그 타입에 관련된 메소드 집합을 가질 수 있다.
[인터페이스 타입(interface type)](/Types/interface_types.html)의 메소드 집합은 인터페이스 자신이다.
이와 다른 타입 T 의 메소드 집합은 수신자(receiver)가 타입 T 인 모든 [메소드(methods)](/Declarations%20and%20scope/method_declarations.html)들로 구성되어 있다. 
[포인터 타입(pointer type)](/Types/pointer_types.html) *T 에 대응되는 메소드 집합은 수신자(receiver)가 *T 또는 T 인 모든 메소드들의 집합으로 구성되어 있다. (따라서, T의 메소드 집합을 포함한다)
embedded fields 를 포함한 구조체에 대해서 적용되는 규칙은 [구조체 타입(struct types)](/Types/struct_types.html) 섹션에서 확인할 수 있다.
이를 제외한 다른 타입들은 빈 메소드 집합을 가지고 있다.
메소드 집합 안에서 각 메소드는 [유일(unique)](/Declarations%20and%20scope/uniqueness_of_identifiers.html)하고 [공백(blank)](/Declarations%20and%20scope/blank_identifier.html)이 아닌 [메소드 이름(method name)](/Types/interface_types.html#MethodName)을 가져야 한다.

The method set of a type determines the interfaces that the type [implements](/Types/interface_types.html) and the methods that can be [called](/Expressions/calls.html) using a receiver of that type.

타입의 메소드 집합은 그 타입이 [구현(implements)](/Types/interface_types.html)하는 인터페이스와 그 타입의 수신자(receiver)를 사용하여 [호출](/Expressions/calls.html)될 수 있는 메소드를 결정한다.