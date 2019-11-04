# Slice

```go
package main

import "fmt"

func main() {
  var slice = []int{1,3,5,6}
  slice = append(slice,8)
  fmt.Println("Capacity",cap(slice))
  fmt.Println("Length",len(slice))
}
```

```go
package main

import "fmt"

func twiceValue(slice []int) {
  var i int
  var value int
  for i,value = range slice {
    slice[i] = 2*value
  }
}

func main() {
  var slice = []int{1,3,5,6}
  twiceValue(slice)
  var i int
  for i=0; i < len(slice); i++ {
    fmt.Println("new slice value",slice[i])
  }
}
```

