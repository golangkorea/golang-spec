# [에러](#errors)

* Go 버전: 1.9
* 원문: [Errors](https://golang.org/ref/spec#Errors)
* 번역자: Jhonghee Park (@jhonghee)

미리 선언된 타입 `error`은 다음과 같이 정의된다.

```
type error interface {
	Error() string
}
```

에러 조건을 표현하기 위한 관례적 인터페이스로 nil 값은 에러가 없음을 나타낸다. 예를 들어, 파일에서 데이터를 읽는 함수는 다음과 같이 정의 될 수 있다:

```
func Read(f *File, b []byte) (n int, err error)
```