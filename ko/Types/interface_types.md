# [interface 타입(Interface types)](#interface-types)

* Go 버전: 1.9
* 원문: [Interface types](https://golang.org/ref/spec#Interface_types)
* 번역자: Jhonghee Park (@jhonghee)

An interface type specifies a [method set](/Types/method_sets.html) called its *interface*. A variable of interface type can store a value of any type with a method set that is any superset of the interface. Such a type is said to *implement the interface*. The value of an uninitialized variable of interface type is `nil`.

interface 타입은 *인터페이스*라고 불리는 [메서드 집합(method set)](/Types/method_sets.html)을 명시한다. 주어진 인터페이스의 확대집합(superset)에 해당하는 메서드 집합을 갖고 있는 어떠한 타입의 값이든 interface 타입의 변수에 저장할 수 있다. 그러한 타입에 대해서는 *인터페이스를 구현*했다라고 말한다. 초기화되지 않은 interface 타입의 변수는 nil 값을 갖는다.

<pre>
<a id="InterfaceType">InterfaceType</a>      = "interface" "{" { <a href="#MethodSpec">MethodSpec</a> ";" } "}" .
<a id="MethodSpec">MethodSpec</a>         = <a href="#MethodName">MethodName</a> <a href="/Types/function_types.html#Signature">Signature</a> | <a href="#InterfaceTypeName">InterfaceTypeName</a> .
<a id="MethodName">MethodName</a>         = <a href="/Lexical%20elements/identifiers.html">identifier</a> .
<a id="InterfaceTypeName">InterfaceTypeName</a>  = <a href="/Types/#TypeName">TypeName</a> .
</pre>

As with all method sets, in an interface type, each method must have a [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html) non-[blank](/Declarations%20and%20scope/blank_identifier.html) name.

모든 메서드 집합에서 그런 것 처럼, interface 타입내, 각 메서드는 [blank 식별자(blank identifier)](/Declarations%20and%20scope/blank_identifier.html)가 아닌 [고유](/Declarations%20and%20scope/uniqueness_of_identifiers.html)한 명칭을 가져야 한다.

```
// A simple File interface
interface {
	Read(b Buffer) bool
	Write(b Buffer) bool
	Close()
}
```

More than one type may implement an interface. For instance, if two types `S1` and `S2` have the method set

한 인터페이스는 여러 타입으로 구현될 수도 있다. 예를 들어, 만약 타입 `S1`와 `S2`가 다음과 같은 메서드 집합을 가지고 있다면

```
func (p T) Read(b Buffer) bool { return … }
func (p T) Write(b Buffer) bool { return … }
func (p T) Close() { … }
```

(where `T` stands for either `S1` or `S2`) then the `File` interface is implemented by both `S1` and `S2`, regardless of what other methods `S1` and `S2` may have or share.

(위에서 `T`는 `S1`일 수도 있고 `S2`일 수도 있다) 이들이 가지고 있거나 공유하고 있는 다른 메서드들과는 상관없이 `S1`과 `S2`는 `File` 인터페이스를 구현한 것이다.

A type implements any interface comprising any subset of its methods and may therefore implement several distinct interfaces. For instance, all types implement the *empty interface*:

타입은 자신의 메서드에 인터페이스의 메서드를 포함시키는 방법을 통해 어떠한 인터페이스든지 구현할 수 있기 때문에 여러 인터페이스를 함께 구현하는 것도 가능하다. 예를 들어, 모든 타입은 empty interface를 구현하고 있다:

```
interface{}
```

Similarly, consider this interface specification, which appears within a [type declaration](/Declarations%20and%20scope/type_declarations.html) to define an interface called `Locker`:

추가로, `Locker`라는 인터페이스를 정의한 [타입 선언문](/Declarations%20and%20scope/type_declarations.html)내 열거되어 있는 인터페이스 사양을 보자. 

```
type Locker interface {
	Lock()
	Unlock()
}
```

If `S1` and `S2` also implement

만약 `S1`과 `S2`가 아래의 메서드도 구현했다면

```
func (p T) Lock() { … }
func (p T) Unlock() { … }
```

they implement the `Locker` interface as well as the `File` interface.

이들은 `File` 인터페이스 뿐만 아니라 `Locker` 인터페이스도 구현한 것이다.

An interface `T` may use a (possibly qualified) interface type name `E` in place of a method specification. This is called *embedding* interface `E` in `T`; it adds all (exported and non-exported) methods of `E` to the interface `T`.

인터페이스 `T`는 메서드의 사양이 있어야 할 자리에 (경우에 따라서는 패키지 이름을 동반한) interface 타입 이름 `E`를 사용할 수도 있다. 이것을 `T`안에 인터페이스 `E`를 *임베딩*했다고 부른다; 임베딩은 (엑스포트 여부에 상관없이) `E`의 모든 메서드를 인터페이스 `T`에 추가한다. 

```
type ReadWriter interface {
	Read(b Buffer) bool
	Write(b Buffer) bool
}

type File interface {
	ReadWriter  // same as adding the methods of ReadWriter
	Locker      // same as adding the methods of Locker
	Close()
}

type LockedFile interface {
	Locker
	File        // illegal: Lock, Unlock not unique
	Lock()      // illegal: Lock not unique
}
```

```
type ReadWriter interface {
	Read(b Buffer) bool
	Write(b Buffer) bool
}

type File interface {
	ReadWriter  // ReadWriter의 메서드를 추가한 것과 같음
	Locker      // Locker의 메서드를 추가한 것과 같음
	Close()
}

type LockedFile interface {
	Locker
	File        // 허용안됨: Lock, Unlock이 고유하지 않음
	Lock()      // 허용안됨: Lock이 고유하지 않음
}
```

An interface type `T` may not embed itself or any interface type that embeds `T`, recursively.

인터페이스 `T`는 자신을 임베딩할 수 없고 `T`를 임베딩한 다른 어떤 인터페이스 타입도 재귀적으로 임베딩할 수 없다.

```
// illegal: Bad cannot embed itself
type Bad interface {
	Bad
}

// illegal: Bad1 cannot embed itself using Bad2
type Bad1 interface {
	Bad2
}
type Bad2 interface {
	Bad1
}
```

```
// 허용안됨: Bad는 자신을 임베딩할 수 없음
type Bad interface {
	Bad
}

// 허용안됨: Bad1은 Bad2를 이용해 임베딩할 수 없음
type Bad1 interface {
	Bad2
}
type Bad2 interface {
	Bad1
}
```