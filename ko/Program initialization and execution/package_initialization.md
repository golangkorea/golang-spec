# [패키지 초기화(Package initialization)](#package-initialization)

* Go 버전: 1.9
* 원문: [Package initialization](https://golang.org/ref/spec#Package_initialization)
* 번역자: Jhonghee Park (@jhonghee)

Within a package, package-level variables are initialized in *declaration order* but after any of the variables they *depend* on.

패키지내 패키지 레벨의 변수들은 *의존하고* 있는 모든 변수들이 초기화되고 난 후 *선언된 순서*에 따라 초기화된다.

More precisely, a package-level variable is considered *ready for initialization* if it is not yet initialized and either has no [initialization expression](/Declarations and scope/variable_declarations.html) or its initialization expression has no dependencies on uninitialized variables. Initialization proceeds by repeatedly initializing the next package-level variable that is earliest in declaration order and ready for initialization, until there are no variables ready for initialization.

더 정확하게 설명하자면, 패키지 레벨의 변수는 아직 초기화가 되지 않은 상태에서 만약 [초기화 식](/Declarations and scope/variable_declarations.html)이 없거나, 있다해도 다른 초기화되지 않은 변수에 대한 의존도가 없다면 *초기화 준비가 된 상태*로 간주한다. 패키지 레벨 변수의 초기화는 더이상 초기화할 준비가 된 변수가 존재하지 않을 때까지, 선언문에 먼저 나타나는 순서대로 반복해서 진행된다.

If any variables are still uninitialized when this process ends, those variables are part of one or more initialization cycles, and the program is not valid.

만약 이 과정이 종료되었음에도 여전히 초기화되지 못한 변수가 남아 있다면, 그런 변수들은 이후 발생할 한번 이상의 추가적인 초기화 사이클에 속하며, 아직 프로그램은 유효하지 않다.

The declaration order of variables declared in multiple files is determined by the order in which the files are presented to the compiler: Variables declared in the first file are declared before any of the variables declared in the second file, and so on.

다수의 파일에 선언된 변수들의 선언순서는 파일들이 컴파일러에 제출된 순서에 따라 정해 진다: 첫번째 파일에 선언된 변수들이 두번째 파일에 선언된 변수보다 먼저 선언되는 식이다.

Dependency analysis does not rely on the actual values of the variables, only on lexical *references* to them in the source, analyzed transitively. For instance, if a variable x's initialization expression refers to a function whose body refers to variable y then x depends on y. Specifically:

  * A reference to a variable or function is an identifier denoting that variable or function.
  * A reference to a method `m` is a [method value](/Expressions/method_values.html) or [method expression](/Expressions/method_expressions.html) of the form `t.m`, where the (static) type of `t` is not an interface type, and the method `m` is in the [method set](/Types/method_sets.html) of `t`. It is immaterial whether the resulting function value `t.m` is invoked.
  * A variable, function, or method `x` depends on a variable `y` if `x`'s initialization expression or body (for functions and methods) contains a reference to `y` or to a function or method that depends on `y`.

의존성에 대한 분석은 변수들의 실제값들에 의지하지 않고, 단지 소스내 변수들을 언급하는 어휘적 *레퍼런스*(lexical *references*)에 의해 전이적으로 (transitively) 분석된다. 예를 들어, 만약에 변수 x의 초기화 식이 함수를 언급하고 함수의 몸통이 변수 y를 언급한다면, x는 y에 의존하는 것이다. 구체적으로:

 * 변수나 함수에 대한 레퍼런스는 변수나 함수를 표시하는 식별자이다.
 * 메서드 `m`에 대한 레퍼런스는 [메서드 값](/Expressions/method_values.html)이거나 `t.m` 형태의 [메서드 식](/Expressions/method_expressions.html)으로, `t`의 (정적) 타입은 인터페이스 타입이 아니고, 메서드 `m`은 `t`의 [메서드 집합](/Types/method_sets.html)에 존재한다. 결과적인 함수 값 `t.m`이 호출되었는지 여부는 중요하지 않다.
 * 변수, 함수, 혹은 메서드 `x`가 변수 `y`에 의존적이라 함은 `x`의 초기화 식이나 (함수들이나 메서드들의) 몸통이 `y`에 대해 레퍼런스를 가지고 있던지 `y`에 의존적인 함수나 메서드에 레퍼런스를 가지고 있는 경우다.

Dependency analysis is performed per package; only references referring to variables, functions, and methods declared in the current package are considered.

의존성 분석은 패키지 단위로 이행되며; 현재의 패키지내 선언되어 있는 변수들, 함수들, 그리고 메서드들을 언급하는 레퍼런스들만 고려된다.

For example, given the declarations

예를 들어, 다음과 같이 주어진 선언문에서

```
var (
	a = c + b
	b = f()
	c = f()
	d = 3
)

func f() int {
	d++
	return d
}
```

the initialization order is d, b, c, a.

초기화 순서는 d, b, c, a이다.

Variables may also be initialized using functions named init declared in the package block, with no arguments and no result parameters.

또한 변수들은 패키지 블럭내 선언된 init이라는 이름의 함수들을 사용해 초기화 될 수 있다. init 함수들은 인수와 리턴값을 갖지 않는다.

```
func init() { … }
```

Multiple such functions may be defined, even within a single source file. The `init` identifier is not [declared](/Declarations and scope/) and thus `init` functions cannot be referred to from anywhere in a program.

심지어 한 소스 파일내 이러한 함수를 여럿 정의할 수 있다. `init`은 [선언된](/Declarations and scope/) 식별자가 아니어서 `init` 함수들은 프로그램의 다른 어떤 곳에서도 언급될 수 없다.

A package with no imports is initialized by assigning initial values to all its package-level variables followed by calling all `init` functions in the order they appear in the source, possibly in multiple files, as presented to the compiler. If a package has imports, the imported packages are initialized before initializing the package itself. If multiple packages import a package, the imported package will be initialized only once. The importing of packages, by construction, guarantees that there can be no cyclic initialization dependencies.

임포트가 없는 패키지의 초기화는 다음과 같다. 우선 패키지 레벨의 변수들에 초기값이 할당되면 소스코드에 나타나는 순서대로 `init` 함수들이 차례로 호출된다. 이런 과정은 여러 파일이 존재하는 경우에도 컴파일에 제출되는 순서에 따라 동일하게 진행된다. 패키지내 임포트가 있는 경우는, 우선 임포트된 패키지가 먼저 초기화된 후 현재 패키지가 초기화된다. 만약 다수의 패키지가 동일한 패키지를 임포트 한 경우, 임포트된 패키지는 한번만 초기화된다. 패키지들을 임포트 하는 과정은 이렇게 잘 짜맞추는 방식을 통해서 순환적으로 초기화하는 의존관계(cyclic initialization dependencies)가 발생하지 않도록 보장한다.

Package initialization—variable initialization and the invocation of `init` functions—happens in a single goroutine, sequentially, one package at a time. An `init` function may launch other goroutines, which can run concurrently with the initialization code. However, initialization always sequences the `init` functions: it will not invoke the next one until the previous one has returned.

패키지 초기화-변수의 초기화와 `init` 함수들의 호출-는 단일 고루틴내에서 발생하며, 한번에 한 패키지씩 순차적으로 일어난다. `init` 함수내에서 다른 고루틴들을 시작할 수도 있는데, 그럴 경우 초기화 코드와 동시에 실행할 수 있다. 하지만 초기화는 항상 `init` 함수들을 순차적으로 실행한다: 이전의 init이 리턴될 때까지 다음 init을 호출하지 않는다.

To ensure reproducible initialization behavior, build systems are encouraged to present multiple files belonging to the same package in lexical file name order to a compiler.

재생가능한 초기화 행동을 보증하기 위해서, 동일한 패키지에 속한 다수의 파일들은 이름에 따라 어휘적으로 순서가 매겨져서 컴파일러에 제출된다. 