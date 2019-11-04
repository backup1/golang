# Multi-dimensional Array

Golang rand is not a real random algorithm. Try to run the following program several times to check. Enjoy. :-\)

```go
package main

import (
  "fmt"
  "math/rand"
)

func main() {
  var threedarray [2][2][2]int
  var i,j,k int
  for i = 0; i < 2; i++ {
    for j = 0; j < 2; j++ {
      for k = 0; k < 2; k++ {
        threedarray[i][j][k] = rand.Intn(3)
      }
    }
  }
  fmt.Println(threedarray)
}
```

