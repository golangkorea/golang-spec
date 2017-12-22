# [여러 인자를 ...매개변수로 넘기기(Passing arguments to ... parameters)](#passing-arguments-to-parameters) {#passing-arguements-to-parameters}

* Go 버전: 1.9
* 원문: [Passing arguments to ...parameters](https://golang.org/ref/spec#Passing_arguments_to_..._parameters)
* 번역자: [조석규](@ezaurum)

If f is [variadic](/Types/function_types.html) with a final parameter p of type ...T, then within f the type of p is equivalent to type []T. If f is invoked with no actual arguments for p, the value passed to p is nil. Otherwise, the value passed is a new slice of type []T with a new underlying array whose successive elements are the actual arguments, which all must be [assignable](/Properties%20of%20types%20and%20values/assignability.html) to T. The length and capacity of the slice is therefore the number of arguments bound to p and may differ for each call site.

만일 `f`가 마지막 매개변수 `p`의 타입이 `...T`인 [가변 인자 함수](/Types/function_types.html)라면, `f` 안에서 `p`의 타입은 `[]T` 타입과 동일하다. 만일 `f`가 `p`에 해당하는 인자 없이 호출된다면, `p`에 `nil`값이 들어간다. 인자가 있는 경우, `[]T` 타입의 새 슬라이스가 넘겨진다. 슬라이스에 내재된 배열은 실제 인자와 같은 값을 가지는데, 각 인자는 모두 T에 [할당 가능](/Properties%20of%20types%20and%20values/assignability.html) 해야 한다. 각 호출시점에 `p`에 할당된 인자의 수에 따라 슬라이스의 길이와 캐퍼시티가 달라진다.

Given the function and calls

주어진 함수를 다음과 같이 호출하면,

```
func Greeting(prefix string, who ...string)
Greeting("nobody")
Greeting("hello:", "Joe", "Anna", "Eileen")
```

within Greeting, who will have the value nil in the first call, and []string{"Joe", "Anna", "Eileen"} in the second.

`Greeting` 안에서 `who`는 첫 번째 호출에는 `nil`이고, 두 번째에는 `[]string{"Joe", "Anna", "Eileen"}`가 된다.

If the final argument is assignable to a slice type []T, it may be passed unchanged as the value for a ...T parameter if the argument is followed by .... In this case no new slice is created.

마지막 인자가 타입 `[]T`의 슬라이스에 할당가능하면, 인자 뒤에 ...을 붙여서 ...T 매개변수의 값으로 그대로 넘길 수 있다. 이 경우 새 슬라이스가 생기지 않는다.

Given the slice s and call

주어진 슬라이스 `s`를 이용해서 다음과 같이 호출하면,

```
s := []string{"James", "Jasmine"}
Greeting("goodbye:", s...)
```

within Greeting, who will have the same value as s with the same underlying array.

`Greeting` 안에서 `who`는 s와 같은 값으로 같은 내재된 배열을 갖게 된다.
