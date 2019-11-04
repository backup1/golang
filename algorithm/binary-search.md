# Binary Search

Complexity $$O(\log n)$$ 

The example below is wrong, because we need to apply binary search on a **sorted** array.

```go
package main

import (
  "fmt"
  "sort"
)

func main() {
  var elements []int = []int{1,3,16,10,45,31,28,36,45,75}
  var element int = 36
  var i int = sort.Search(len(elements), func(i int) bool { return elements[i] >= element })
  if i < len(elements) && elements[i] == element {
    fmt.Printf("found element %d at index %d in %v\n",element,i,elements)
  } else {
    fmt.Printf("element %d not found in %v\n",element,elements)
  }
}
```

