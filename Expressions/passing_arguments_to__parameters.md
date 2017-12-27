# 여러 인자를 ...매개변수로 넘기기(Passing arguments to ... parameters) {#passing-arguements-to-parameters}

* Go 버전: 1.9
* 원문: [Passing arguments to ...parameters](https://golang.org/ref/spec#Passing_arguments_to_..._parameters)
* 번역자: [조석규](@ezaurum)

If f is [variadic](/Types/function_types.html) with a final parameter p of type ...T, then within f the type of p is equivalent to type []T. If f is invoked with no actual arguments for p, the value passed to p is nil. Otherwise, the value passed is a new slice of type []T with a new underlying array whose successive elements are the actual arguments, which all must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to T. The length and capacity of the slice is therefore the number of arguments bound to p and may differ for each call site.

마지막 매개변수 `p`가 `...T` 타입인 [가변 인자 함수](/Types/function_types.html) `f`의 내부에서는 매개변수 `p`의 타입이 `[]T`와 같다. 함수 `f` 호출시 매개변수 `p`에 해당하는 인자들이 없다면, 매개변수 `p`에는 `nil` 값이 전달된다. 인자가 있는 경우, `[]T` 타입의 새 슬라이스가 넘겨진다. 슬라이스의 내재 배열은 새로 생성되며 실제 인자와 같은 값을 가지므로, 각 인자는 모두 `T`에 [할당 가능](/Properties%20of%20types%20and%20values/assignability.html)해야 한다. 슬라이스의 길이와 용량(capacity)은 각 호출 시점에 매개변수 `p`에 할당된 인자의 수에 따라 달라진다.

Given the function and calls

`Greeting` 함수를 다음과 같이 호출했을 때,

```
func Greeting(prefix string, who ...string)
Greeting("nobody")
Greeting("hello:", "Joe", "Anna", "Eileen")
```

within Greeting, who will have the value nil in the first call, and []string{"Joe", "Anna", "Eileen"} in the second.

`Greeting` 함수 안에서 `who`는 첫 번째 호출에서는 `nil`값을, 두 번째 호출 때는 `[]string{"Joe", "Anna", "Eileen"}`값을 갖는다.

If the final argument is assignable to a slice type []T, it may be passed unchanged as the value for a ...T parameter if the argument is followed by .... In this case no new slice is created.

마지막 인자를 슬라이스 타입 `[]T`에 할당할 수 있다면, 인자 뒤에 `...`을 붙여서 이 인자를 그대로 `...T` 매개변수에 대한 값으로 전달할 수 있다. 이 경우에는 새로운 슬라이스가 생성되지 않는다.

Given the slice s and call

슬라이스 `s`에 대해 다음과 같이 호출했을 때,

```
s := []string{"James", "Jasmine"}
Greeting("goodbye:", s...)
```

within Greeting, who will have the same value as s with the same underlying array.

`Greeting` 함수 안에서 `who`는 `s` 와 같은 값을 가질 것이고, 내재 배열도 `s`와 같을 것이다.
