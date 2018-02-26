# [타입 선언](#type-declarations)

타입 선언문은 식별자인, *타입 이름*을 <a href="#Types">타입</a>에 바인딩한다. 타입 선언문은 두 가지 형태가 있다: 별명 선언과 타입 정의.

<pre>
<a id="TypeDecl">TypeDecl</a> = "type" ( <a href="#TypeSpec">TypeSpec</a> | "(" { (<a href="#TypeSpec">TypeSpec</a> ";" } ")" ) .
<a id="TypeSpec">TypeSpec</a> = <a href="#AliasDecl">AliasDecl</a> | <a href="#TypeDef">TypeDef</a> .
</pre>

## [별명 선언](#alias-declarations)

별명 선언은 식별자를 주어진 타입에 바인딩한다.

<pre>
<a id="AliasDecl">AliasDecl</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> "=" <a href="#Type">Type</a> .
</pre>

식별자의 [범위](/Declarations%20and%20scope/) 내에서는, 그 타입의 *별명*으로 사용된다.

```go
type (
    nodeList = []*Node  // nodeList 와 []*Node 는 동일한 타입이다.
    Polar    = polar    // Polar 와 polar 는 동일한 타입을 나타낸다.
)
```

## [타입 정의](#type-definitions)

타입 정의는 주어진 타입과 같은 [내재 타입](/Types/)과 연산를 갖는 새롭고, 구별되는 타입을 만들고, 그 것에 식별자를 바인딩한다.

<pre>
<a id="TypeDef">TypeDef</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> <a href="/Types/#Type">Type</a> .
</pre>

새로운 타입은 *타입 정의를 통해 만든 타입*이라고 부른다. 어느 다른 타입과도 [다른](Properties%20of%20types%20and%20values/type_identity.html) 것이며, 심지어 만들기 위해 사용했던 타입과도 다르다.

```go
type (
    Point struct{ x, y float64 }  // Point 와 struct{ x, y float64 } 은 다른 타입이다.
    polar Point                   // polar 와 Point 는 다른 타입을 나타낸다.
)

type TreeNode struct {
    left, right *TreeNode
    value *Comparable
}

type Block interface {
    BlockSize() int
    Encrypt(src, dst []byte)
    Decrypt(src, dst []byte)
}
```
타입 정의를 이용해 만든 타입은 연관된 [메서드들](/Declarations%20and%20scope/method_declarations.html)이 있을 수 있다. 주어진 타입에 바인딩된 메서드는 상속하지 않지만, 인터페이스 타입의 [메서드 집합](/Types/method_sets.html) 이나 합성 타입의 요소들의 메서드들은 변동없이 남는다.

```go
// A Mutex is a data type with two methods, Lock and Unlock.
type Mutex struct         { /* Mutex 필드들 */ }
func (m *Mutex) Lock()    { /* Lock 구현 */ }
func (m *Mutex) Unlock()  { /* Unlock 구현 */ }

// NewMutex는 Mutex와 같은 구성이지만 메서드 집합은 비어있다.
type NewMutex Mutex

// PtrMutex의 기본 타입의 메서드 집합은 변동없이 남는다,
// 하지만 PtrMutex의 메서드 집합은 비어있다.
type PtrMutex *Mutex

// *PrintableMutex의 메서드 집합은 임베딩된 필드 Mutex에 바인딩된 Lock과 Unlock의 메서드들을 포함한다.
type PrintableMutex struct {
    Mutex
}

// MyBlock는 인터페이스 타입으로 Block과 같은 메서드 집합을 가지고 있다.
type MyBlock Block
```

타입 정의는 별개의 불리어, 숫자, 혹은 문자열 타입을 정의할 수 있고, 그 것들에 메서드도 연결시킬 수 있다.

```go
type TimeZone int

const (
    EST TimeZone = -(5 + iota)
    CST
    MST
    PST
)

func (tz TimeZone) String() string {
    return fmt.Sprintf("GMT%+dh", tz)
}
```
