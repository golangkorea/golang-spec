# [타입 선언문](#type-declarations)

타입 선언문은 식별자인 *타입 이름*을 <a href="#Types">타입</a>과 연결한다. 타입 선언문은 두 가지 형태가 있다: 별칭 선언문과 타입 정의.

<pre>
<a id="TypeDecl">TypeDecl</a> = "type" ( <a href="#TypeSpec">TypeSpec</a> | "(" { (<a href="#TypeSpec">TypeSpec</a> ";" } ")" ) .
<a id="TypeSpec">TypeSpec</a> = <a href="#AliasDecl">AliasDecl</a> | <a href="#TypeDef">TypeDef</a> .
</pre>

## [별칭 선언문](#alias-declarations)

별칭 선언문은 식별자를 특정 타입과 연결한다.

<pre>
<a id="AliasDecl">AliasDecl</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> "=" <a href="#Type">Type</a> .
</pre>

식별자의 [범위](/Declarations%20and%20scope/) 내에서 타입에 대한 *별칭* 으로 사용된다.

```go
type (
    nodeList = []*Node  // nodeList 와 []*Node 는 같은 타입이다.
    Polar    = polar    // Polar 와 polar 는 같은 타입을 나타낸다.
)
```

## [타입 정의](#type-definitions)

타입 정의는 식별자를 특정 타입과 연결하며, 해당 타입과 같은 [내재 타입](/Types/)과 연산을 가진 새롭고, 고유한 타입을 만든다. 

<pre>
<a id="TypeDef">TypeDef</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> <a href="/Types/#Type">Type</a> .
</pre>

이렇게 생성된 타입을 *타입 정의를 이용해 만든 타입(defined type)* 이라고 부른다. 이 타입은 다른 타입과 [다른](Properties%20of%20types%20and%20values/type_identity.html) 고유한 타입이며, 타입을 만들기 위해 사용했던 타입과 다르다.

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
타입 정의를 이용해 만든 타입은 [메서드](/Declarations%20and%20scope/method_declarations.html)를 가질 수 있다. 타입 정의에 사용했던 타입과 관련된 메서드는 상속받지 않지만, interface 타입의 [메서드 집합](/Types/method_sets.html) 또는 합성 타입 요소들의 메서드 집합은 그대로 유지된다.

```go
// Mutex 는 Lock, Unlock 등 두 개의 메서드를 가진 데이터 타입이다.
type Mutex struct         { /* Mutex 필드들 */ }
func (m *Mutex) Lock()    { /* Lock 구현 */ }
func (m *Mutex) Unlock()  { /* Unlock 구현 */ }

// NewMutex는 Mutex와 같은 합성이지만 메서드 집합은 비어있다.
type NewMutex Mutex

// PtrMutex의 기본 타입은 메서드 집합은 그대로 유지된다.
// 하지만 PtrMutex의 메서드 집합은 비어있다.
type PtrMutex *Mutex

// *PrintableMutex의 메서드 집합은 임베디드 필드 Mutex에 관련된 Lock, Unlock 메서드를 포함한다.
type PrintableMutex struct {
    Mutex
}

// MyBlock는 interface 타입이며 Block과 같은 메서드 집합을 가지고 있다.
type MyBlock Block
```

타입 정의는 불리언, 숫자, string 타입과 이들 타입과 관련된 메서드를 다르게 정의하는데 사용할 수도 있다.

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
