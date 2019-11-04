# Decorator

```go
package main

import "fmt"

type IProcess interface {
  process()
}

type ProcessClass struct {}

func (process *ProcessClass) process() {
  fmt.Println("ProcessClass process")
}

type ProcessDecorator struct {
  processInstance *ProcessClass
}

func (decorator *ProcessDecorator) process() {
  if decorator.processInstance == nil {
    fmt.Println("ProcessDecorator process")
  } else {
    fmt.Printf("ProcessDecorator process and ")
    decorator.processInstance.process()
  }
}

func main() {
  var process = &ProcessClass{}
  var decorator = &ProcessDecorator{}
  decorator.process()
  decorator.processInstance = process
  decorator.process()
}
```

