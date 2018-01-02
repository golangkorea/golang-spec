# [여러 인자를 ...매개변수로 넘기기](#passing-arguements-to-parameters)

마지막 매개변수 `p`가 `...T` 타입인 [가변 인자 함수](/Types/function_types.html) `f`의 내부에서는 매개변수 `p`의 타입이 `[]T`와 같다. 함수 `f` 호출시 매개변수 `p`에 해당하는 인자들이 없다면, 매개변수 `p`에는 `nil` 값이 전달된다. 인자가 있는 경우, `[]T` 타입의 새 슬라이스가 넘겨진다. 슬라이스의 내재 배열은 새로 생성되며 실제 인자와 같은 값을 가지므로, 각 인자는 모두 `T`에 [할당 가능](/Properties%20of%20types%20and%20values/assignability.html)해야 한다. 슬라이스의 길이와 용량(capacity)은 각 호출 시점에 매개변수 `p`에 할당된 인자의 수에 따라 달라진다.

`Greeting` 함수를 다음과 같이 호출했을 때,

```
func Greeting(prefix string, who ...string)
Greeting("nobody")
Greeting("hello:", "Joe", "Anna", "Eileen")
```

`Greeting` 함수 안에서 `who`는 첫 번째 호출에서는 `nil`값을, 두 번째 호출 때는 `[]string{"Joe", "Anna", "Eileen"}`값을 갖는다.

마지막 인자를 슬라이스 타입 `[]T`에 할당할 수 있다면, 인자 뒤에 `...`을 붙여서 이 인자를 그대로 `...T` 매개변수에 대한 값으로 전달할 수 있다. 이 경우에는 새로운 슬라이스가 생성되지 않는다.

슬라이스 `s`에 대해 다음과 같이 호출했을 때,

```
s := []string{"James", "Jasmine"}
Greeting("goodbye:", s...)
```

`Greeting` 함수 안에서 `who`는 `s` 와 같은 값을 가질 것이고, 내재 배열도 `s`와 같을 것이다.
