# Doubly Linked List

Golang list container is a doubly linked list.

```go
package main

import (
  "container/list"
  "fmt"
)

func main() {
  var linkedList *list.List = list.New()
  var element *list.Element = linkedList.PushBack(14)
  var frontElement *list.Element = linkedList.PushFront(1)
  linkedList.InsertBefore(6,element)
  linkedList.InsertAfter(5,frontElement)
  var crtElement *list.Element
  for crtElement = linkedList.Front(); crtElement != nil; crtElement = crtElement.Next() {
    fmt.Println(crtElement.Value)
  }
}
```

```go
package main

import "fmt"

type Node struct {
  property int
  nextNode *Node
  previousNode *Node
}

type LinkedList struct {
  headNode *Node
}

func (linkedList *LinkedList) NodeBetweenValues(firstProperty int,secondProperty int) *Node {
  var node *Node
  var nodeWith *Node
  for node = linkedList.headNode; node != nil; node = node.nextNode {
    if node.previousNode != nil && node.nextNode != nil {
      if node.previousNode.property == firstProperty && node.nextNode.property == secondProperty {
        nodeWith = node
        break;
      }
    }
  }
  return nodeWith
}

func (linkedList *LinkedList) AddToHead(property int) {
  var node = &Node{}
  node.property = property
  node.nextNode = nil
  node.nextNode = linkedList.headNode
  if linkedList.headNode != nil {
    linkedList.headNode.previousNode = node
  }
  linkedList.headNode = node
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
    node.previousNode = nodeWith
    nodeWith.nextNode.previousNode = node
    nodeWith.nextNode = node
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
  node.previousNode = nil
  var lastNode *Node = linkedList.LastNode()
  if lastNode != nil {
    lastNode.nextNode = node
    node.previousNode = lastNode
  } else {
    linkedList.headNode = node
  }
}

func main() {
  var linkedList LinkedList
  linkedList = LinkedList{}
  linkedList.AddToHead(1)
  linkedList.AddToHead(3)
  linkedList.AddToEnd(5)
  linkedList.AddAfter(1,7)
  fmt.Println(linkedList.headNode.property)
  var node *Node
  node = linkedList.NodeBetweenValues(1,5)
  fmt.Println(node.property)
}
```

