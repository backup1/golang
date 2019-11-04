# 2D Slice

```go
package main

import "fmt"

func main() {
  var TwoDArray [8][8]int
  TwoDArray[3][6] = 18
  TwoDArray[7][4] = 3
  fmt.Println(TwoDArray)
}
```

```go
package main

import "fmt"

func main() {
  var rows int
  var cols int
  rows = 7
  cols = 9
  var twodslices = make([][]int,rows)
  var i int
  for i = range twodslices {
    twodslices[i] = make([]int,cols)
  }
  fmt.Println(twodslices)
}
```

```go
package main

import "fmt"

func main() {
  var arr = []int{5,6,7,8,9}
  var sl1 = arr[:3]
  fmt.Println("slice1",sl1)
  var sl2 = arr[1:5]
  fmt.Println("slice2",sl2)
  var sl3 = append(sl2,12)
  fmt.Println("slice3",sl3)
}
```

