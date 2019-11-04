# Tree

```go
package main

import "fmt"

type Tree struct {
  LeftNode *Tree
  Value int
  RightNode *Tree
}

func (tree *Tree) insert(m int) {
  if tree == nil {
    tree = &Tree{nil,m,nil}
  } else if tree.LeftNode == nil {
    tree.LeftNode = &Tree{nil,m,nil}
  } else if tree.RightNode == nil {
    tree.RightNode = &Tree{nil,m,nil}
  } else if tree.LeftNode != nil {
    tree.LeftNode.insert(m)
  } else {
    tree.RightNode.insert(m)
  }
}

func print(tree *Tree,indent int) {
  if tree != nil {
    fmt.Println(" Value",tree.Value)
    for i := 0; i < indent; i++ {
      fmt.Printf("  ")
    }
    fmt.Printf("Tree Node Left")
    print(tree.LeftNode,indent+1)
    for i := 0; i < indent; i++ {
      fmt.Printf("  ")
    }
    fmt.Printf("Tree Node Right")
    print(tree.RightNode,indent+1)
  } else {
    fmt.Printf(" Nil\n")
  }
}

func main() {
  var tree *Tree = &Tree{nil,1,nil}
  tree.insert(3)
  tree.insert(5)
  tree.LeftNode.insert(7)
  print(tree,0)
}
```

