# Circular Linked List / Ring

```go
package main

import (
  "container/ring"
  "fmt"
)

func main() {
  var integers []int = []int{1,3,5,7}
  var circularList *ring.Ring = ring.New(len(integers))
  var i int
  for i = 0; i < circularList.Len(); i++ {
    circularList.Value = integers[i]
    circularList = circularList.Next()
  }
  circularList.Do(func(element interface{}) {
    fmt.Print(element,",")
  })
  fmt.Println()
  for i = 0; i < circularList.Len(); i++ {
    fmt.Print(circularList.Value,",")
    circularList = circularList.Prev()
  }
  fmt.Println()
  circularList = circularList.Move(2)
  circularList.Do(func(element interface{}) {
    fmt.Print(element,",")
  })
}
```

