# Unordered List

```go
package main

import "fmt"

type Node struct {
  property int
  nextNode *Node
}

type UnOrderedList struct {
  headNode *Node
}

func (unOrderedList *UnOrderedList) AddToHead(property int) {
  var node = &Node{}
  node.property = property
  node.nextNode = nil
  if unOrderedList.headNode != nil {
    node.nextNode = unOrderedList.headNode
  }
  unOrderedList.headNode = node
}

func (unOrderedList *UnOrderedList) IterateList() {
  var node *Node
  for node = unOrderedList.headNode; node != nil; node = node.nextNode {
    fmt.Println(node.property)
  }
}

func main() {
  var unOrderedList UnOrderedList = UnOrderedList{}
  unOrderedList.AddToHead(1)
  unOrderedList.AddToHead(3)
  unOrderedList.AddToHead(5)
  unOrderedList.AddToHead(7)
  unOrderedList.IterateList()
}
```

