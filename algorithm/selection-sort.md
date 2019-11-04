# Selection Sort

Complexity $$O(n^2)$$ 

```go
package main

import "fmt"

func SelectionSorter(elements []int) {
  var i int
  for i = 0; i < len(elements)-i; i++ {
    var min int = i
    var j int
    for j = i+1; j < len(elements); j++ {
      if elements[j] < elements[min] {
        min = j
      }
    }
    elements[i],elements[min] = elements[min],elements[i]
  }
}

func main() {
  var elements []int
  elements = []int{11, 4, 18, 6, 19, 21, 71, 13, 15, 2}
  fmt.Println("Before Sorting ", elements)
  SelectionSorter(elements)
  fmt.Println("After Sorting", elements)
}
```

