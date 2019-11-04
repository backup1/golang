# Logging \(with line number\)

```go
package main

import(
  "path"
  "runtime"
  "fmt"
  "log"
  "time"
)

func checkPoint() string {
  pc, file, line, _ := runtime.Caller(1)
  return fmt.Sprintf("\033[31m%v %s %s line#%d\x1b[0m", time.Now(), runtime.FuncForPC(pc).Name(), path.Base(file), line)
}

func method1(){
  fmt.Println(checkPoint())
}

func main() {
  log.SetFlags(log.LstdFlags | log.Lshortfile)
  log.Println("logging the time and flags")
  method1()
}
```

