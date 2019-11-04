# Merge Sort

The merge sort algorithm is a comparison-based method that was invented by John Von Neumann.

Complexity $$O(n \log n)$$ 

```go
package main

import (
  "fmt"
  "math/rand"
  "time"
)

func createArray(num int) []int {
  var array []int = make([]int,num,num)
  rand.Seed(time.Now().UnixNano())
  var i int
  for i = 0; i < num; i++ {
    array[i] = rand.Intn(99999)-rand.Intn(99999)
  }
  return array
}

func MergeSorter(array []int) []int {
  if len(array) < 2 {
    return array
  }
  var middle int = (len(array))/2
  return JoinArrays(MergeSorter(array[:middle]),MergeSorter(array[middle:]))
}

func JoinArrays(left []int, right []int) []int {
  var num int = len(left)+len(right)
  var i int = 0
  var j int = 0
  var array []int = make([]int,num,num)
  var k int
  for k = 0; k < num; k++ {
    if i > len(left)-1 && j <= len(right)-1 {
      array[k] = right[j];
      j++
    } else if j > len(right)-1 && i <= len(left)-1{
      array[k] = left[i]
      i++
    } else if left[i] < right[j] {
      array[k] = left[i]
      i++
    } else {
      array[k] = right[j]
      j++
    }
  }
  return array
}

func main() {
  var elements []int = createArray(40)
  fmt.Println("\n Before Sorting \n\n", elements)
  fmt.Println("\n-After Sorting\n\n", MergeSorter(elements), "\n")
}
```

