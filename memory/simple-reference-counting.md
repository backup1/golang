# Simple Reference Counting

```go
package main

import (
  "sync/atomic"
  "sync"
  "fmt"
)

type ReferenceCounter struct {
  num *uint32
  pool *sync.Pool
  removed *uint32
}

func newReferenceCounter() ReferenceCounter {
  return ReferenceCounter{
    num: new(uint32),
    pool: &sync.Pool{},
    removed: new(uint32),
  }
}

func (referenceCounter ReferenceCounter) Add() {
  atomic.AddUint32(referenceCounter.num, 1)
}

func (referenceCounter ReferenceCounter) Subtract() {
  if atomic.AddUint32(referenceCounter.num, ^uint32(0)) == 0 {
    atomic.AddUint32(referenceCounter.removed, 1)
  }
}

func main() {
  var referenceCounter ReferenceCounter = newReferenceCounter()
  referenceCounter.Add()
  fmt.Println(*referenceCounter.num)
}
```

