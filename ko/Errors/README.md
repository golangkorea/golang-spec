# [에러](#errors)

미리 선언된 타입 `error`은 다음과 같이 정의된다.

```go
type error interface {
    Error() string
}
```

에러 조건을 표현하기 위한 관례적 인터페이스로 nil 값은 에러가 없음을 나타낸다. 예를 들어, 파일에서 데이터를 읽는 함수는 다음과 같이 정의 될 수 있다:

```go
func Read(f *File, b []byte) (n int, err error)
```