# [pointer 타입(Pointer types)](#pointer-types)

 * Go 버전: 1.9
 * 원문: [Pointer types](https://golang.org/ref/spec#Pointer_types)
 * 번역자: Jhonghee Park (@jhonghee)
 
A pointer type denotes the set of all pointers to [variables](/Variables/) of a given type, called the base *type* of the pointer. The value of an uninitialized pointer is `nil`.

포인터 타입은 주어진 타입의 [변수(variables)](/Variables/)를 가리키는 모든 포인터의 집합을 의미하는데, 이 주어진 타입을 그 포인터의 기초 *타입* (base *type*)이라고 부른다. 초기화되지 않은 포인터의 값은 `nil`이다.

<pre>
<a id="PointerType">PointerType</a> = "*" <a href="#BaseType">BaseType</a> .
<a id="BaseType">BaseType</a>    = <a href="/Types/#Type">Type</a> .
</pre>

```
*Point
*[4]int
```