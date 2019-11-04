# Singly Linked List

```go
package main

import (
  "container/list"
  "fmt"
)

func main() {
  var ilist list.List
  ilist.PushBack(11)
  ilist.PushBack(23)
  ilist.PushBack(34)
  for element := ilist.Front(); element != nil; element = element.Next() {
    fmt.Println(element.Value.(int))
  }
}
```

```go
package main

import "fmt"

type Node struct {
  property int
  nextNode *Node
}

type LinkedList struct {
  headNode *Node
}

func (linkedList *LinkedList) AddToHead(property int) {
  var node = Node{}
  node.property = property
  node.nextNode = linkedList.headNode
  linkedList.headNode = &node
}

func (linkedList *LinkedList) IterateList() {
  var node *Node
  for node = linkedList.headNode; node != nil; node = node.nextNode {
    fmt.Println(node.property)
  }
}

func (linkedList *LinkedList) LastNode() *Node {
  var node *Node
  var lastNode *Node
  for node = linkedList.headNode; node != nil; node = node.nextNode {
    if node.nextNode == nil {
      lastNode = node
    }
  }
  return lastNode
}

func (linkedList *LinkedList) AddToEnd(property int) {
  var node = &Node{}
  node.property = property
  node.nextNode = nil
  var lastNode *Node = linkedList.LastNode()
  if lastNode != nil {
    lastNode.nextNode = node
  } else {
    linkedList.headNode = node
  }
}

func (linkedList *LinkedList) NodeWithValue(property int) *Node {
  var node *Node
  var nodeWith *Node
  for node = linkedList.headNode; node != nil; node = node.nextNode {
    if node.property == property {
      nodeWith = node
      break
    }
  }
  return nodeWith
}

func (linkedList *LinkedList) AddAfter(nodeProperty int,property int) {
  var node = &Node{}
  node.property = property
  node.nextNode = nil
  var nodeWith *Node
  nodeWith = linkedList.NodeWithValue(nodeProperty)
  if nodeWith != nil {
    node.nextNode = nodeWith.nextNode
    nodeWith.nextNode = node
  }
}

func main() {
  var linkedList LinkedList
  linkedList = LinkedList{}
  linkedList.AddToHead(1)
  linkedList.AddToHead(3)
  linkedList.AddToEnd(5)
  linkedList.AddAfter(1,7)
  linkedList.IterateList()
}
```

```go
package main

import "fmt"

type Node struct {
  nextNode *Node
  property rune
}

func CreateLinkedList() *Node {
  var headNode *Node
  headNode = &Node{nil,'a'}
  var crtNode *Node
  crtNode = headNode
  var i rune
  for i = 'b'; i <= 'z'; i++ {
    var node *Node = &Node{nil,i}
    crtNode.nextNode = node
    crtNode = node
  }
  return headNode
}

func ReverseLinkedList(nodeList *Node) *Node {
  var crtNode *Node = nodeList
  var topNode *Node = nil
  for {
    if crtNode == nil {
      break
    }
    var tmpNode *Node = crtNode.nextNode
    crtNode.nextNode = topNode
    topNode = crtNode
    crtNode = tmpNode
  }
  return topNode
}

func stringify(nodeList *Node) {
  if nodeList != nil {
    fmt.Printf("%c",nodeList.property)
    stringify(nodeList.nextNode)
  } else {
    fmt.Println()
  }
}


func main() {
  var linkedList = CreateLinkedList()
  stringify(linkedList)
  stringify(ReverseLinkedList(linkedList))
}
```

