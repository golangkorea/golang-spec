# [예제 패키지](#an-example-package)

다음은 프라임 시브(prime sieve) 알고리즘을 동시적으로 구현한 Go 패키지 전체이다..

```go
package main

import "fmt"

// 2, 3, 4, ... 숫자열을 채널 'ch'로 보낸다.
func generate(ch chan<- int) {
    for i := 2; ; i++ {
        ch <- i  // 'i'를 채널 'ch'에 보낸다.
    }
}

// 'prime'으로 나눌 수 있는 것들은 제거 하면서,
// 채널 'src'에서 채널 'dst'로 값들을 복사한다.
func filter(src <-chan int, dst chan<- int, prime int) {
    for i := range src {  // 'src'로 부터 받은 값들을 루프에서 처리한다.
        if i%prime != 0 {
            dst <- i  // 'i'를 채널 'dst'에 보낸다.
        }
    }
}

// The prime sieve: 데이지-체인 필터가 함께 처리한다.
func sieve() {
    ch := make(chan int)  // 새 채널을 만든다.
    go generate(ch)       // generate()를 하위 프로세스로 시작한다.
    for {
        prime := <-ch
        fmt.Print(prime, "\n")
        ch1 := make(chan int)
        go filter(ch, ch1, prime)
        ch = ch1
    }
}

func main() {
    sieve()
}
```
