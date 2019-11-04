# Heap

```go
package main

import (
  "container/heap"
  "fmt"
)

type IHeap []int

func (iheap IHeap) Len() int {
  return len(iheap)
}

func (iheap IHeap) Less(i,j int) bool {
  return iheap[i] < iheap[j]
}

func (iheap IHeap) Swap(i,j int) {
  iheap[i],iheap[j] = iheap[j],iheap[i]
}

func (iheap *IHeap) Push(heapintf interface{}) {
  *iheap = append(*iheap,heapintf.(int))
}

func (iheap *IHeap) Pop() interface{} {
  var n,x1 int
  var previous IHeap = *iheap
  n = len(previous)
  x1 = previous[n-1]
  *iheap = previous[0:n-1]
  return x1
}

func main() {
  var iheap *IHeap = &IHeap{1,4,5}
  heap.Init(iheap)
  heap.Push(iheap,2)
  fmt.Printf("minimum: %d\n",(*iheap)[0])
  for iheap.Len() > 0 {
    fmt.Printf("%d\n",heap.Pop(iheap))
  }
}
```

