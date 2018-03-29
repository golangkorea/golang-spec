# [타입 변환](#conversions)

타입 변환은 `T(x)`의 형태로 구성된 식(expression)이며, `T`는 타입, `x`는 `T` 타입으로 변환될 수 있는 식을 의미한다.

<pre>
<a id="Conversion">Conversion</a> = <a href="/Types/#Type">Type</a> "(" <a href="/Expressions/operators.html#Expression">Expression</a> [ "," ] ")" .
</pre>

타입이 `*`나 `<-` 연산자로 시작하거나 반환 값 목록이 없는 `func` 키워드로 시작하면 괄호를 추가하여 의도를 명확하게 전달하는 것이 좋다. 

```go
*Point(p)        // *(Point(p))와 같음
(*Point)(p)      // p가 *Point로 변환된 경우
<-chan int(c)    // <-(chan int(c))와 같음
(<-chan int)(c)  // c가 <-chan int로 변환된 경우
func()(x)        // 함수 시그니처 func() x
(func())(x)      // x가 func()로 변환된 경우
(func() int)(x)  // x가 func() int로 변환된 경우
func() int(x)    // x가 func() int로 변환된 경우 (의도가 명확하므로 괄호가 필요없음)
```

아래의 조건을 하나라도 만족하면 [상수](/Constants)값 `x`는 `T` 타입으로 변환될 수 있다:

  * `x`를 `T` 타입의 값으로 나타낼 수 있음.
  * `x`가 부동 소수점 상수이고, `T`는 부동 소수점 타입이며, IEEE 754 가까운 짝수로 반올림하는 규칙과 -0.0을 부호없는 0.0으로 반올림하는 IEEE 규칙을 적용한 `x`는 `T` 타입의 값으로 나타낼 수 있는 경우. 이때, 상수 `T(x)`는 반올림된 값이다.
  * `x`는 정수 상수이고 `T`는 [string 타입](/Types/string_types.html)일 때. 이때는 상수가 아닌 `x` 에 적용하는 [규칙](#conversions-to-and-from-a-string-type)이 사용된다.

상수의 변환 결과는 타입 정보가 있는 상수다.

```go
uint(iota)               // uint 타입의 iota 값
float32(2.718281828)     // float32 타입의 2.718281828
complex128(1)            // complex128 타입의 1.0 + 0.0i
float32(0.49999999)      // float32 타입의 0.5
float64(-1e-1000)        // float64 타입의 0.0
string('x')              // string 타입의 "x"
string(0x266c)           // string 타입의 "♬"
MyString("foo" + "bar")  // MyString 타입의 "foobar"
string([]byte{'a'})      // 상수가 아님: []byte{'a'}은 상수가 아님
(*int)(nil)              // 상수가 아님: nil은 상수가 아님, *int는 불리언 타입, 숫자 타입, string 타입도 아님
int(1.2)                 // 허용안됨: 1.2는 정수로 나타낼 수 없음
string(65.0)             // 허용안됨: 65.0는 정수 상수가 아님
```

아래의 조건을 하나라도 만족하면 상수가 아닌 값 `x`는 `T` 타입으로 변환될 수 있다:

  * `x`를 `T`에 [할당할 수](/Properties%20of%20types%20and%20values/assignability.html) 있음.
  * `x`의 타입과 `T`가 [같은](#Type_identity) [내재 타입](#Types)을 가지고 있을 때. 이때, struct 태그는 무시한다 (아래 참조)
  * struct 태그를 무시하면 (아래 참조), `x`의 타입과 `T`는 [정의가 되지않은](/Declarations%20and%20scope/type_declarations.html#type-definitions) 포인터 타입으로, 같은 내재 타입을 포인터의 기본 타입으로 가진다.
  * `x`'의 타입과 `T`가 둘 다 정수 포인터 타입이거나 부동 소수점 포인터 타입이다.
  * `x`의 타입과 `T`는 둘 다 복소수 타입이다.
  * `x`가 정수이거나, 바이트 슬라이스이거나 룬이고 `T`는 string 타입이다.
  * `x`는 문자열이고 `T`는 바이트 슬라이스이거나 룬이다.

변환을 목적으로 struct 타입의 아이덴티티(identity)를 비교할 때 [Struct 태그](/Struct_types/)는 무시된다.

```go
type Person struct {
    Name    string
    Address *struct {
        Street string
        City   string
    }
}

var data *struct {
    Name    string `json:"name"`
    Address *struct {
        Street string `json:"street"`
        City   string `json:"city"`
    } `json:"address"`
}

var person = (*Person)(data)  // 태그를 무시하면, 내재 타입은 같다
```

(상수가 아닌) 숫자 타입들과 string 타입 사이의 변환은 특별한 규칙들이 적용되는 사례이다. 이런 변환들은 `x`의 표현을 바꿔놓을 수도 있고 런타임 비용을 야기할 수도 있다. 이처럼 `x`의 표현을 바꾸는 경우가 아닌 다른 모든 변환들은 타입만을 변환한다.

포인터와 정수 사이의 변환을 가능케 하는 언어적 메커니즘은 없다. 이러한 기능들은 [unsafe](/Systemonsiderations/package_unsafe.html) 패키지를 통해 제한적인 상황에만 구현된다.

## 숫자 타입 사이의 변환

상수가 아닌 숫자 값들의 변환에는 다음과 같은 규칙들이 적용된다:

  1. 정수 타입 사이에서 변환이 일어날때, 부호 있는 정수값은 무한한 정밀도로 암시적인 확장이 일어날 때 부호비트로 채운다; 부호가 없는 정수값은 확장될 때 제로값으로 채워진다. 그런 다음 변환 결과 타입의 크기에 맡게 재단된다. 예를 들어, `v := uint16(0x10F0)`, 변환 뒤에는 `uint32(int8(v)) == 0xFFFFFFF0`와 같은 결과를 얻는다. 변환은 항상 유효한 값을 산출하고; 오버플로우가 일어나지 않는다.
  2. 부동 소수점 숫자가 정수로 변환될 때, 소수점 이하는 버려진다 (제로 방향으로 잘라냄)
  3. 정수나 부동 소수점 숫자를 부동 소수점 타입으로 변환할 때, 혹은 복소수를 다른 복소수 타입으로 변환할 때, 결괏값은 대상 타입에 의해 지정된 정밀도에 따라 반올림된다. 예를 들어, 타입 `float32`의 변수 `x`의 값은 IEEE-754 32-비트를 초과하는 정밀도로 저장될 수 있지만, `float32(x)`는 `x`의 값이 32 비트 정밀도에 맞게 반올림한 결과를 나타낸다. 비슷하게, `x + 0.1`는 32 비트의 정밀도 이상을 사용할 수도 있지만, `float32(x + 0.1)`은 그렇지 않다.

부동 소수점 값이나 복소수 값에 관련된 상수가 아닌 모든 변환에서, 결과의 타입이 값을 나타내지 못하는 경우라면 변환은 성공하지만 결괏값은 구현에 따라 달라진다.

## string 타입으로 변환, 그리고 string 타입으로 부터의 변환

  1. 부호가 있건 없건 정수값을 string 타입으로 변환하면 정수의 UTF-8 표현을 포함하는 문자열을 산출한다. 유니코드 포인트들의 범위밖에 있는 값들은 "\uFFFD"로 변환된다.
<pre>
string('a')       // "a"
string(-1)        // "\ufffd" == "\xef\xbf\xbd"
string(0xf8)      // "\u00f8" == "ø" == "\xc3\xb8"
type MyString string
MyString(0x65e5)  // "\u65e5" == "日" == "\xe6\x97\xa5"
</pre>
  2. 바이트 슬라이스를 string 타입으로 변환해서 산출된 문자열의 연속적인 바이트들은 슬라이스의 요소들이다.
<pre>
string([]byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'})   // "hellø"
string([]byte{})                                     // ""
string([]byte(nil))                                  // ""
&nbsp;
type MyBytes []byte
string(MyBytes{'h', 'e', 'l', 'l', '\xc3', '\xb8'})  // "hellø"
</pre>
  3. 룬 슬라이스를 string 타입으로 변환해서 산출된 문자열은 각각의 룬 값들의 연결을 문자열로 변환한 것이다.
<pre>
string([]rune{0x767d, 0x9d6c, 0x7fd4})   // "\u767d\u9d6c\u7fd4" == "白鵬翔"
string([]rune{})                         // ""
string([]rune(nil))                      // ""
&nbsp;
type MyRunes []rune
string(MyRunes{0x767d, 0x9d6c, 0x7fd4})  // "\u767d\u9d6c\u7fd4" == "白鵬翔"
</pre>
  4. string 타입의 값을 바이트 타입의 슬라이스로 변환하여 산출된 슬라이스는 연속하는 요소들이 문자열의 바이트들이다.
<pre>
[]byte("hellø")   // []byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'}
[]byte("")        // []byte{}
&nbsp;
MyBytes("hellø")  // []byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'}
</pre>
  5. string 타입의 값을 룬 타입의 슬라이스로 변환하여 산출된 슬라이스는 문자열의 개별 유니코드 포인트들을 포함하고 있다.
<pre>
[]rune(MyString("白鵬翔"))  // []rune{0x767d, 0x9d6c, 0x7fd4}
[]rune("")                 // []rune{}
&nbsp;
MyRunes("白鵬翔")           // []rune{0x767d, 0x9d6c, 0x7fd4}
</pre>
