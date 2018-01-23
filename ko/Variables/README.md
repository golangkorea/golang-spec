# [변수](#variables)

변수는 어떤 값을 저장해 놓을 수 있는 저장소다. 값이 저장가능한 지의 여부는 변수의 *[타입](/Types/)* 에 의해 결정된다.

[변수의 선언](/Declarations%20and%20scope/variable_declarations.html) 및 함수 인자들과 함수의 결과 값들, [함수 선언](/Declarations%20and%20scope/function_declarations.html)의 시그니처 또는 [함수 리터럴](/Expressions/function_literals.html)은 명명된 변수를 위해 저장소에 자리를 잡아둔다. built-in 함수인 [new](/Built-in%20functions/allocation.html)를 부르거나 [합성 리터럴(composite literal)](/Expressions/composite_literals.html)의 주소를 가져오는 것으로 변수를 실행 시간에 저장소에 할당할 수 있다. 이러한 익명의 변수는 (암묵적으로) [포인터](/Expressions/address_operators.html) 를 통해 참조된다.

*구조화된* 변수인 [array](/Types/array_types.html), [slice](/Types/slice_types.html)와 [struct](/Types/struct_types.html) 타입들은 개별적인 [주소](/Expressions/address_operators.html)가 있는 요소와 필드를 가진다. 이러한 각각의 요소들은 변수처럼 동작한다.

어떤 변수의 *static 타입* (또는 그냥 *타입*)은 `new` 호출 또는 composite literal에서 제공받은 타입이거나 구조화된 변수 요소의 타입이 해당 변수의 선언중에 할당된 것이다. interface 타입의 변수들은 또한 분명한 *동적 타입*, 즉, 런타임에(미리 선언된 식별자 `nil` 같은 타입이 없는 값만 아니면) 변수에 할당된 값의 콘크리트 타입을 가지고 있다. 동적 타입은 실행 되는 동안 달라지겠지만 interface 변수들에 저장된 값들은 항상 해당 변수의 static 타입에 [할당될 수(assignable)](/Properties%20of%20types%20and%20values/assignability.html) 있다.

```go
var x interface{}  // x는 nil 이면서 interface{}형 static 타입을 가진다
var v *T           // v는 nil 값을 *T형 static 타입으로 가진다
x = 42             // x는 값 42를 int형 동적 타입으로 가진다
x = v              // x는 (*T)(nil)를 *T형 동적 타입으로 가진다
```

변수의 값은 [식](/Expressions/)에 있는 변수를 참조함으로서 검색된다. 이것은 가장 최근에 해당 변수에 [할당된](/Statements/assignments.html) 값이다. 만약 아직 값이 변수에 할당되어지지 않았다면 변수의 값은 해당 변수의 타입을 위해 [zero값](/Program%20initialization%20and%20execution/the_zero_value.html)이 된다.