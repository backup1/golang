# AVL Tree

AVL is named after Adelson, Velski, and Landis.

The code example below contains bug. Please feel free to fix it. Thanks

```go
package main

import (
  "fmt"
  "encoding/json"
)

type KeyValue interface {
  LessThan(KeyValue) bool
  EqualTo(KeyValue) bool
}

type TreeNode struct {
  keyValue KeyValue
  balanceValue int
  linkedNodes [2]*TreeNode
}

func opposite(nodeValue int) int {
  return 1-nodeValue
}

func singleRotation(rootNode *TreeNode,nodeValue int) *TreeNode {
  var saveNode *TreeNode
  saveNode = rootNode.linkedNodes[opposite(nodeValue)]
  rootNode.linkedNodes[opposite(nodeValue)] = saveNode.linkedNodes[nodeValue]
  saveNode.linkedNodes[nodeValue] = rootNode
  return saveNode
}

func doubleRotation(rootNode *TreeNode,nodeValue int) *TreeNode {
  var saveNode *TreeNode
  saveNode = rootNode.linkedNodes[opposite(nodeValue)].linkedNodes[nodeValue]
  rootNode.linkedNodes[opposite(nodeValue)].linkedNodes[nodeValue] = saveNode.linkedNodes[opposite(nodeValue)]
  saveNode.linkedNodes[opposite(nodeValue)] = rootNode.linkedNodes[opposite(nodeValue)]
  rootNode.linkedNodes[opposite(nodeValue)] = saveNode
  saveNode = rootNode.linkedNodes[opposite(nodeValue)]
  rootNode.linkedNodes[opposite(nodeValue)] = saveNode.linkedNodes[nodeValue]
  saveNode.linkedNodes[nodeValue] = rootNode
  return saveNode
}

func adjustBalance(rootNode *TreeNode,nodeValue int,balanceValue int) {
  var node *TreeNode
  node = rootNode.linkedNodes[nodeValue]
  var oppNode *TreeNode
  oppNode = node.linkedNodes[opposite(balanceValue)]
  switch oppNode.balanceValue {
  case 0:
    rootNode.balanceValue = 0
    node.balanceValue = 0
  case balanceValue:
    rootNode.balanceValue = -balanceValue
    node.balanceValue = 0
  default:
    rootNode.balanceValue = 0
    node.balanceValue = balanceValue
  }
  oppNode.balanceValue = 0
}

func BalanceTree(rootNode *TreeNode,nodeValue int) *TreeNode {
  var node *TreeNode
  node = rootNode.linkedNodes[nodeValue]
  var balance int
  balance = 2*nodeValue - 1
  if node.balanceValue == balance {
    rootNode.balanceValue = 0
    node.balanceValue = 0
    return singleRotation(rootNode,opposite(nodeValue))
  }
  adjustBalance(rootNode,nodeValue,balance)
  return doubleRotation(rootNode,opposite(nodeValue))
}

func insertRNode(rootNode *TreeNode,key KeyValue) (*TreeNode, bool) {
  if rootNode == nil {
    return &TreeNode{keyValue:key},false
  }
  var dir int
  dir = 0
  if rootNode.keyValue.LessThan(key) {
    dir = 1
  }
  var done bool
  rootNode.linkedNodes[dir],done = insertRNode(rootNode.linkedNodes[dir],key)
  if done {
    return rootNode,true
  }
  rootNode.balanceValue += 2*dir - 1
  switch rootNode.balanceValue {
  case 0:
    return rootNode, true
  case 1, -1:
    return rootNode, false
  }
  return BalanceTree(rootNode,dir),true
}

func InsertNode(treeNode **TreeNode,key KeyValue) {
  *treeNode,_ = insertRNode(*treeNode,key)
}

func RemoveNode(treeNode **TreeNode,key KeyValue) {
  *treeNode,_ = removeRNode(*treeNode,key)
}

func removeBalance(rootNode *TreeNode,nodeValue int) (*TreeNode, bool) {
  var node *TreeNode
  node = rootNode.linkedNodes[opposite(nodeValue)]
  var balance int
  balance = 2*nodeValue - 1
  switch node.balanceValue {
  case -balance:
    rootNode.balanceValue = 0
    node.balanceValue = 0
    return singleRotation(rootNode,nodeValue),false
  case balance:
    adjustBalance(rootNode,opposite(nodeValue),-balance)
    return doubleRotation(rootNode,nodeValue),false
  }
  rootNode.balanceValue = -balance
  node.balanceValue = balance
  return singleRotation(rootNode,nodeValue),true
}

func removeRNode(rootNode *TreeNode,key KeyValue) (*TreeNode, bool) {
  if rootNode == nil {
    return nil,false
  }
  if rootNode.keyValue.EqualTo(key) {
    switch {
    case rootNode.linkedNodes[0] == nil:
      return rootNode.linkedNodes[1],false
    case rootNode.linkedNodes[1] == nil:
      return rootNode.linkedNodes[0],false
    }
    var heirNode *TreeNode = rootNode.linkedNodes[0]
    for heirNode.linkedNodes[1] != nil {
      heirNode = heirNode.linkedNodes[1]
    }
    rootNode.keyValue = heirNode.keyValue
    key = heirNode.keyValue
  }
  var dir int = 0
  if rootNode.keyValue.LessThan(key) {
    dir = 1
  }
  var done bool
  rootNode.linkedNodes[dir],done = removeRNode(rootNode.linkedNodes[dir],key)
  if done {
    return rootNode,true
  }
  rootNode.balanceValue += 1 - 2*dir
  switch rootNode.balanceValue {
  case 1, -1:
    return rootNode,true
  case 0:
    return rootNode,false
  }
  return removeBalance(rootNode,dir)
}

type integerKey int
func (k integerKey) LessThan(k1 KeyValue) bool {
  return k < k1.(integerKey)
}
func (k integerKey) EqualTo(k1 KeyValue) bool {
  return k == k1.(integerKey)
}

func main() {
  var treeNode *TreeNode
  fmt.Println("Tree is empty")
  var avlTree []byte
  avlTree,_ = json.MarshalIndent(treeNode,""," ")
  fmt.Println(string(avlTree))
  fmt.Println("\n Add Tree")
  InsertNode(&treeNode,integerKey(5))
  InsertNode(&treeNode,integerKey(3))
  InsertNode(&treeNode,integerKey(8))
  InsertNode(&treeNode,integerKey(7))
  InsertNode(&treeNode,integerKey(6))
  InsertNode(&treeNode,integerKey(10))
  avlTree,_ = json.MarshalIndent(treeNode,""," ")
  fmt.Println(string(avlTree))
  fmt.Println("\n Delete Tree")
  RemoveNode(&treeNode,integerKey(3))
  RemoveNode(&treeNode,integerKey(7))
  avlTree,_ = json.MarshalIndent(treeNode,""," ")
  fmt.Println(string(avlTree))
}
```

