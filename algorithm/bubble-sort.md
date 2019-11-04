# Bubble Sort

Complexity $$O(n^2)$$ 

```go
package main

import "fmt"

func bubbleSorter(integers [11]int) {
  var num int = 11
  var isSwapped bool = true
  for isSwapped {
    isSwapped = false
    var i int
    for i = 1; i < num; i++ {
      if integers[i-1] > integers[i] {
        integers[i],integers[i-1] = integers[i-1],integers[i]
        isSwapped = true
      }
    }
  }
  fmt.Println(integers)
}

func main() {
  var integers [11]int = [11]int{31, 13, 12, 4, 18, 16, 7, 2, 3, 0, 10}
  fmt.Println("Bubble Sorter")
  bubbleSorter(integers)
}
```

