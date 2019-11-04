# TreeSet

```go
package main

type TreeSet struct {
  bst *BinarySearchTree
}

func (treeSet *TreeSet) InsertTreeNode(treeNodes ...TreeNode) {
  var treeNode TreeNode
  for _,treeNode = range treeNodes {
    treeSet.bst.InsertElement(treeNode.key,treeNode.value)
  }
}

func (treeSet *TreeSet) Delete(treeNodes ...TreeNode) {
  var treeNode TreeNode
  for _,treeNode = range treeNodes {
    treeSet.bst.RemoveNode(treeNode.key)
  }
}

/*func (tree *BinarySearchTree) InOrderTraverseTree(function func(int)) {
  tree.lock.RLock()
  defer tree.lock.RUnlock()
  inOrderTraverseTree(tree.rootNode,function)
}*/

/*func inOrderTraverseTree(treeNode *TreeNode,function func(int)) {
  if treeNode != nil {
    inOrderTraverseTree(treeNode.leftNode,function)
    function(treeNode.value)
    inOrderTraverseTree(treeNode.rightNode,function)
  }
}*/

/*func (tree *BinarySearchTree) PreOrderTraverseTree(function func(int)) {
  tree.lock.Lock()
  defer tree.lock.Unlock()
  preOrderTraverseTree(tree.rootNode,function)
}*/

/*func preOrderTraverseTree(treeNode *TreeNode,function func(int)) {
  if treeNode != nil {
    function(treeNode.value)
    preOrderTraverseTree(treeNode.leftNode,function)
    preOrderTraverseTree(treeNode.rightNode,function)
  }
}*/

func (treeSet *TreeSet) Search(treeNodes ...TreeNode) bool {
  var treeNode TreeNode
  var exists bool
  for _,treeNode = range treeNodes {
    if exists = treeSet.bst.SearchNode(treeNode.key); !exists {
      return false
    }
  }
  return true
}

func (treeSet *TreeSet) String() {
  treeSet.bst.String()
}

func main() {
  var treeset *TreeSet = &TreeSet{}
  treeset.bst = &BinarySearchTree{}
  var node1 TreeNode = TreeNode{8,8, nil,nil}
  var node2 TreeNode = TreeNode{3,3,nil, nil}
  var node3 TreeNode = TreeNode{10,10,nil,nil}
  var node4 TreeNode = TreeNode{1,1,nil,nil}
  var node5 TreeNode = TreeNode{6,6,nil,nil}
  treeset.InsertTreeNode(node1,node2,node3, node4, node5)
  treeset.String()
}
```

As the above program uses the code of Binary Search Tree, the compilation and execution is slighty different:

```bash
$ go build treeset.go binarysearchtree.go

$ ./treeset.exe
------------------------------------------------
        ***> 1
    ***> 3
        ***> 6
***> 8
    ***> 10
------------------------------------------------
```

Synchronized TreeSet

```go
func (tree *BinarySearchTree) InsertElement(key int,value int) {
  tree.lock.Lock()
  defer tree.lock.Unlock()
  var treeNode *TreeNode
  treeNode = &TreeNode{key,value,nil,nil}
  if tree.rootNode == nil {
    tree.rootNode = treeNode
  } else {
    insertTreeNode(tree.rootNode,treeNode)
  }
}
```

Mutable TreeSet

```go
func insertTreeNode(rootNode *TreeNode, newTreeNode *TreeNode) {
  if newTreeNode.key < rootNode.key {
    if rootNode.leftNode == nil {
      rootNode.leftNode = newTreeNode
    } else {
      insertTreeNode(rootNode.leftNode, newTreeNode)
    }
  } else {
    if rootNode.rightNode == nil {
      rootNode.rightNode = newTreeNode
    } else {
      insertTreeNode(rootNode.rightNode, newTreeNode)
    }
  }
}

func (tree *BinarySearchTree) RemoveNode(key int) {
  tree.lock.Lock()
  defer tree.lock.Unlock()
  removeNode(tree.rootNode, key)
}

func main() {
  var treeset *TreeSet = &TreeSet{}
  treeset.bst = &BinarySearchTree{}
  var node1 TreeNode = TreeNode{8, 8, nil, nil}
  var node2 TreeNode = TreeNode{3, 3, nil, nil}
  var node3 TreeNode = TreeNode{10, 10, nil, nil}
  var node4 TreeNode = TreeNode{1, 1, nil, nil}
  var node5 TreeNode = TreeNode{6, 6, nil, nil}
  treeset.InsertTreeNode(node1, node2, node3, node4, node5)
  treeset.String()
}
```

