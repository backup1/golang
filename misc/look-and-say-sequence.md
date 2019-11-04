# Look and Say sequence

```go
package main

import (
  "fmt"
  "strconv"
)

func looksay(str string) (rstr string) {
  var cbyte byte = str[0]
  var inc int = 1
  var i int
  for i = 1; i < len(str); i++ {
    var dbyte byte = str[i]
    if dbyte == cbyte {
      inc++
      continue
    }
    rstr += strconv.Itoa(inc) + string(cbyte)
    cbyte = dbyte
    inc = 1
  }
  return rstr + strconv.Itoa(inc) + string(cbyte)
}

func main() {
  var str string = "1"
  fmt.Println(str)
  var i int
  for i = 0; i < 8; i++ {
    str = looksay(str)
    fmt.Println(str)
  }
}
```

