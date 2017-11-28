# Program execution

# 프로그램 실행

A complete program is created by linking a single, unimported package called the *main package* with all the packages it imports, transitively. The main package must have package name `main` and declare a function `main` that takes no arguments and returns no value.

*main 패키지*는 임포트되지 않는 유일한 패키지이다. Go 프로그램은 이러한 main 패키지를 그 자체내 임포트된 모든 패키지와 연결함으로써 완성되는데, 각 패키지내의 임포트된 패키지도 이 과정에서 함께 연결된다. main 패키지는 `main`이라는 패키지  이름을 사용하여야만 하며 `main` 함수를 선언하되 인수가 없고 리턴값도 없다.

```
func main() { … }
```

Program execution begins by initializing the main package and then invoking the function `main`. When that function invocation returns, the program exits. It does not wait for other (non-`main`) goroutines to complete.

프로그램의 실행은 main 패키지를 초기화한 후 `main` 함수를 실행함으로 시작된다. main 함수가 리턴되면 실행은 종료된다. 실행의 종료를 위해 다른 (`main`이 아닌) 고루틴을 기다리지 않는다.