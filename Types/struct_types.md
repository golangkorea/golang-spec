# [struct 타입(Struct types)](#struct-types)

* Go 버전: 1.9
* 원문 : [Struct types](https://golang.org/ref/spec#Struct_types)
* 번역자 : [연규민](@voidsatisfaction)

A struct is a sequence of named elements, called fields, each of which has a name and a type. Field names may be specified explicitly (IdentifierList) or implicitly (EmbeddedField). Within a struct, non-[blank](/Declarations%20and%20scope/blank_identifier.html) field names must be [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html).

구조체는 필드(fields)의 연속이다. 필드는 이름과 타입을 갖고 있다. 필드의 이름은 명시적으로 지정되거나(IdentifierList) 암묵적으로 지정된다(임베드된 필드 EmbeddedField). 구조체 내부에는, non-[blank](/Declarations%20and%20scope/blank_identifier.html)인 필드 이름은 반드시 [유일](/Declarations%20and%20scope/uniqueness_of_identifiers.html)해야한다.

<pre>
<a id="StructType">StructType</a>     = "struct" "{" { <a href="#FieldDecl">FieldDecl</a> ";" } "}" .
<a id="FieldDecl">FieldDecl</a>      = (<a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> <a href="/Types/#Type">Type</a> | <a href="#EmbeddedField">EmbeddedField</a>) [ <a href="#Tag">Tag</a> ] .
<a id="EmbeddedField">EmbeddedField</a> = [ "*" ] <a href="/Types/#TypeName">TypeName</a> .
<a id="Tag">Tag</a>            = <a href="/Lexical%20elements/string_literals.html#string_lit">string_lit</a> .
</pre>

```
// An empty struct.
struct {}

// A struct with 6 fields.
struct {
	x, y int
	u float32
	_ float32  // padding
	A *[]int
	F func()
}
```

```
// 빈 구조체.
struct {}

// 6개의 필드를 가진 구조체.
struct {
	x, y int
	u float32
	_ float32  // 패딩(padding)
	A *[]int
	F func()
}
```

A field declared with a type but no explicit field name is an *embedded field*. An embedded field must be specified as a type name `T` or as a pointer to a non-interface type name `*T`, and `T` itself may not be a pointer type. The unqualified type name acts as the field name.

*임베드된 필드(embedded field)* 란 타입으로 선언되었으나 명시적인 이름이 없는 필드를 말한다. 임베드된 필드는 타입 이름 `T`로 지정되거나 인터페이스가 아닌 타입 이름 `*T`, 그리고 `T` 그자체가 포인터 타입이 아닐 수 있다. unqualified된 타입 이름이 필드 이름으로 될 수 있다.

```
// A struct with four embedded fields of types T1, *T2, P.T3 and *P.T4
struct {
	T1        // field name is T1
	*T2       // field name is T2
	P.T3      // field name is T3
	*P.T4     // field name is T4
	x, y int  // field names are x and y
}
```

```
// 타입 T1, *T2, P.T3, P.T4가 임베드된 4개의 필드를 가진 구조체
struct {
	T1        // 필드 이름은 T1
	*T2       // 필드 이름은 T2
	P.T3      // 필드 이름은 T3
	*P.T4     // 필드 이름은 T4
	x, y int  // 필드 이름은 각각 x와 y
}
```

The following declaration is illegal because field names must be unique in a struct type:

아래와 같은 선언은 구조체의 필드 이름이 반드시 유일해야 하기 때문에 허용되지 않는다:

```
struct {
	T     // 임베드된 필드 *T, *P.T와 충돌
	*T    // 임베드된 필드 T, *P.T와 충돌
	*P.T  // 임베드된 필드 T, *T와 충돌
}
```

A field or [method](/Declarations%20and%20scope/method_declarations.html) f of an embedded field in a struct x is called promoted if x.f is a legal [selector](/Expressions/selectors.html) that denotes that field or method f.

구조체 `x`에 임베드된 필드 혹은 [메서드](/Declarations%20and%20scope/method_declarations.html) `f`는 `x.f`가 필드 혹은 [메서드](/Declarations%20and%20scope/method_declarations.html)를 의미하는 유효한 selector인 경우, 이를 promoted라고 불린다.

Promoted fields act like ordinary fields of a struct except that they cannot be used as field names in [composite literals](/Expressions/composite_literals.html) of the struct.

promoted 필드는 구조체의 [합성 리터럴](/Expressions/composite_literals.html)에서 필드 이름으로 사용 될 수 없는 것을 제외하고 일반적인 필드 처럼 행동한다.

Given a struct type `S` and a type named `T`, promoted methods are included in the method set of the struct as follows:

  * If `S` contains an embedded field T, the [method sets](/Types/method_sets.html) of S and `*S` both include promoted methods with receiver T. The method set of `*S` also includes promoted methods with receiver `*T`.
  * If `S` contains an embedded field `*T`, the method sets of S and `*S` both include promoted methods with receiver T or `*T`.

구조체 타입 `S`와 타입 이름 `T`가 주어졌을때, promoted 메서드는 아래와 같이 구조체의 메서드 집합(method set)에 포함된다:

  * 만약 `S`가 임베드된 필드 `T`를 표함하면, S와 `*S`의 [메서드 집합](/Types/method_sets.html)은 receiver `T`와 함께 promoted 메서드를 포함한다. `*S`의 메서드 셋 역시 receiver `T`와 함께 promoted 메서드를 포함한다.
  * 만약 `S`가 임베드된 필드 `*T`를 포함하면, S와 `*S`의 메서드 집합은 receiver `T`,`*T`와 함께 promoted 메서드를 포함한다.

A field declaration may be followed by an optional string literal tag, which becomes an attribute for all the fields in the corresponding field declaration. An empty tag string is equivalent to an absent tag. The tags are made visible through a [reflection interface](https://golang.org/pkg/reflect/#StructTag) and take part in [type identity](/Properties%20of%20types%20and%20values/type_identity.html) for structs but are otherwise ignored.

필드 선언에 문자열 리터럴 태그를 선택적으로 놓을 수 있다. 그리고 그 태그는 해당하는 필드 선언의 모든 필드를 위한 속성이 된다. 공백의 태그 문자열은 태그가 없는 것과 같다. 태그들은 [reflection interface](https://golang.org/pkg/reflect/#StructTag)를 통해서 볼 수 있고, 구조체의 [타입 식별자](/Properties%20of%20types%20and%20values/type_identity.html)에 참여하나 그렇지 않은 경우는 무시된다.

```
struct {
	x, y float64 ""  // an empty tag string is like an absent tag
	name string  "any string is permitted as a tag"
	_    [4]byte "ceci n'est pas un champ de structure"
}

// A struct corresponding to a TimeStamp protocol buffer.
// The tag strings define the protocol buffer field numbers;
// they follow the convention outlined by the reflect package.
struct {
	microsec  uint64 `protobuf:"1"`
	serverIP6 uint64 `protobuf:"2"`
}
```

```
struct {
	x, y float64 ""  // 공백 태그 문자열은 태그가 없는 것과 같다.
	name string  "any string is permitted as a tag"
	_    [4]byte "ceci n'est pas un champ de structure"
}

// TimeStamp protocol buffer와 대응하는 구조체.
// 태그 문자열은 protocol buffer 필드 숫자를 정의하며
// reflect 패키지에 의해 구체화된 관습을 따른다.
struct {
	microsec  uint64 `protobuf:"1"`
	serverIP6 uint64 `protobuf:"2"`
}
```
