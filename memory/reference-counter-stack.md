# Reference Counter / Stack

```go
package main

import (
  "fmt"
  "sync"
)

type ReferenceCounter struct {
  num *uint32
  pool *sync.Pool
  removed *uint32
}

func NewReferenceCounter() *ReferenceCounter {
  return &ReferenceCounter{
    num: new(uint32),
    pool: &sync.Pool{},
    removed: new(uint32),
  }
}

type Stack struct {
  references []*ReferenceCounter
  Count int
}

func (stack *Stack) New() {
  stack.references = make([]*ReferenceCounter,0)
}

func (stack *Stack) Push(reference *ReferenceCounter) {
  stack.references = append(stack.references[:stack.Count],reference)
  stack.Count++
}

func (stack *Stack) Pop() *ReferenceCounter {
  if stack.Count == 0 {
    return nil
  }
  var length int = len(stack.references)
  var reference *ReferenceCounter = stack.references[length-1]
  if length > 1 {
    stack.references = stack.references[:length-1]
  } else {
    stack.references = stack.references[0:]
  }
  stack.Count = len(stack.references)
  return reference
}

func main() {
  var stack *Stack = &Stack{}
  stack.New()
  var reference1 *ReferenceCounter = NewReferenceCounter()
  var reference2 *ReferenceCounter = NewReferenceCounter()
  var reference3 *ReferenceCounter = NewReferenceCounter()
  var reference4 *ReferenceCounter = NewReferenceCounter()
  stack.Push(reference1)
  stack.Push(reference2)
  stack.Push(reference3)
  stack.Push(reference4)
  fmt.Println(stack.Pop(),stack.Pop(),stack.Pop(),stack.Pop())
}
```

