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
  *  `x`의 타입과 `T`가 포인터 타입일 때. 이때 포인터 타입은 [타입 정의를 이용해 만든 타입](/Declarations%20and%20scope/type_declarations.html#type-definitions)이 아니며, 이들의 포인터 기본 타입이 같은 내재 타입인 경우. struct 태그는 무시한다 (아래 참조),
  * `x`'의 타입과 `T`가 둘 다 정수 포인터 타입이거나 부동 소수점 포인터 타입일 때.
  * `x`의 타입과 `T`가 둘 다 복소수 타입일 때.
  * `x`가 정수, byte 슬라이스, 룬 타입 중 하나이고 `T`는 string 타입일 때.
  * `x`는 문자열 타입이고 `T`는 byte 슬라이스 또는 룬 타입일 때.

변환을 목적으로 struct 타입의 아이덴티티(identity)를 비교할 때 [struct 태그](/Struct_types/)는 무시된다.

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

(상수가 아닌) 숫자 타입간의 변환, 상수가 아닌 타입과 string 타입 사이의 변환에는 특별한 규칙이 적용된다. 이런 변환은 `x`의 표현을 바꿀 수도 있고 런타임 비용을 야기할 수도 있다. 이밖의 변환은 타입만 변경할 뿐 `x`의 표현을 바꾸지는 않는다.

포인터와 정수를 서로 변환할 수 있는 언어적 메커니즘은 없다. [unsafe](/Systemonsiderations/package_unsafe.html) 패키지는 제한된 상황에서 이 기능을 구현했다.

## 숫자 타입 사이의 변환

상수가 아닌 숫자 값들의 변환에는 다음과 같은 규칙들이 적용된다:

  1. 정수 타입 사이에서 변환이 일어날 때, 부호 있는 정숫값은 내부적으로 무한 정밀도로 확장될 때 부호 비트로 채워진다; 부호가 없는 정수값은 확장될 때 제로값으로 채워진다. 그런 다음 변환 결과 타입 크기에 맞게 길이가 조정된다(truncated). 예를 들어, `v := uint16(0x10F0)` 의 변환 결과는 `uint32(int8(v)) == 0xFFFFFFF0`와 같다. 변환은 항상 유효한 값을 산출하며 오버플로우가 발생하지 않는다.
  2. 부동 소수점 숫자가 정수로 변환될 때, 소수점 이하는 버려진다 (0 기준으로 잘림)
  3. 정수나 부동 소수점 숫자를 부동 소수점 타입으로 변환할 때, 혹은 복소수를 다른 복소수 타입으로 변환할 때, 결괏값은 대상 타입에 의해 지정된 정밀도에 따라 반올림된다. 예를 들어, `float32` 타입의 변수 `x`의 값은 IEEE-754 32-비트 숫자를 초과하는 정밀도로 저장될 수 있지만, `float32(x)`는 32 비트 정밀도로 `x`의 값을 반올림한 결과로 나타난다. 이와 유사하게, `x + 0.1`는 32 비트 정밀도를 능가하는 숫자를 사용할 수도 있지만, `float32(x + 0.1)`은 그렇지 않다.

상수가 아닌 부동 소수점 값이나 복소수 값에 대한 모든 변환에서, 결과의 타입을 값으로 표현할 수 없더라도 변환은 성공한 것이지만 결괏값은 구현에 따라 달라진다.

## string 타입으로 변환과 string 타입에 대한 변환

  1. 부호가 있거나 없는 정숫값을 string 타입으로 변환하면 해당 정수의 UTF-8 표현이 담긴 문자열이 된다. 유효한 유니코드 코드 포인트 범위를 벗어난 값은 "\uFFFD"로 변환된다.
<pre>
string('a')       // "a"
string(-1)        // "\ufffd" == "\xef\xbf\xbd"
string(0xf8)      // "\u00f8" == "ø" == "\xc3\xb8"
type MyString string
MyString(0x65e5)  // "\u65e5" == "日" == "\xe6\x97\xa5"
</pre>
  2. byte 슬라이스를 string 타입으로 변환하면 문자열이 되고 이 문자열의 연속적인 byte는 슬라이스의 요소들이다.
<pre>
string([]byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'})   // "hellø"
string([]byte{})                                     // ""
string([]byte(nil))                                  // ""
&nbsp;
type MyBytes []byte
string(MyBytes{'h', 'e', 'l', 'l', '\xc3', '\xb8'})  // "hellø"
</pre>
  3. 룬 슬라이스를 string 타입으로 변환하면 문자열이 되고 이 문자열은 각 룬 값들을 문자열로 변환한 것을 합친 것이다.
<pre>
string([]rune{0x767d, 0x9d6c, 0x7fd4})   // "\u767d\u9d6c\u7fd4" == "白鵬翔"
string([]rune{})                         // ""
string([]rune(nil))                      // ""
&nbsp;
type MyRunes []rune
string(MyRunes{0x767d, 0x9d6c, 0x7fd4})  // "\u767d\u9d6c\u7fd4" == "白鵬翔"
</pre>
  4. string 타입의 값을 byte 타입의 슬라이스로 변환하면 슬라이스가 되고 이 슬라이스의 연속된 요소들은 문자열의 바이트다.
<pre>
[]byte("hellø")   // []byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'}
[]byte("")        // []byte{}
&nbsp;
MyBytes("hellø")  // []byte{'h', 'e', 'l', 'l', '\xc3', '\xb8'}
</pre>
  5. string 타입의 값을 룬 타입의 슬라이스로 변환하면 슬라이스가 되고 이 슬라이스는 문자열의 개별 유니코드 코드 포인트를 담고 있다.
<pre>
[]rune(MyString("白鵬翔"))  // []rune{0x767d, 0x9d6c, 0x7fd4}
[]rune("")                 // []rune{}
&nbsp;
MyRunes("白鵬翔")           // []rune{0x767d, 0x9d6c, 0x7fd4}
</pre>
