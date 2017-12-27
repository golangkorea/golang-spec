# [프로그램 실행(Program execution)](#program-execution)

* Go 버전: 1.9
* 원문: [Program execution](https://golang.org/ref/spec#Program_execution)
* 번역자: Jhonghee Park (@jhonghee)

A complete program is created by linking a single, unimported package called the *main package* with all the packages it imports, transitively. The main package must have package name `main` and declare a function `main` that takes no arguments and returns no value.

Go 프로그램은 임포트되지 않은 단일의 `main` 패키지에 main이 임포트한 모든 패키지를 연결(link)함으로 써 완성되는데, 이러한 연결은 임포트되는 패키지내부에서도 일어난다. main 패키지는 `main`이라는 패키지 이름을 사용하여야만 하며 인자값과 반환값이 없는 `main` 함수를 선언해야 한다.

```
func main() { … }
```

Program execution begins by initializing the main package and then invoking the function `main`. When that function invocation returns, the program exits. It does not wait for other (non-`main`) goroutines to complete.

프로그램 실행은 main 패키지를 초기화하고, `main` 함수를 호출하면서 시작된다.
main 함수 호출이 반환되면 프로그램이 종료되며, `main` 이외의 고루틴 작업이 완료되지 않더라도 프로그램은 종료된다.