# Panic, Recover and Defer

```go
package main

import "fmt"

func main() {
  panicTest(true)
  fmt.Println("hello world")
}

func checkPanic() {
  if r := recover(); r != nil {
    fmt.Println("A Panic was captured, message:", r)
  }
}

func panicTest(p bool) {
  // in here we use a combination of defer and recover
  defer checkPanic()
  if p {
    panic("panic requested")
  }
}
```

