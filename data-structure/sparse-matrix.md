# Sparse Matrix

```go
package main

import "fmt"

type ListOfList struct {
  Row int
  Column int
  Value float64
}

type SparseMatrix struct {
  cells []ListOfList
  shape [2]int
}

func (sparseMatrix *SparseMatrix) Shape() (int,int) {
  return sparseMatrix.shape[0],sparseMatrix.shape[1]
}

func (sparseMatrix *SparseMatrix) NumNonZero() int {
  return len(sparseMatrix.cells)
}

func LessThan(lol ListOfList, i int, j int) bool {
  if lol.Row < i && lol.Column < j {
    return true
  }
  return false
}

func Equal(lol ListOfList, i int, j int) bool {
  if lol.Row == i && lol.Column == j {
    return true
  }
  return false
}

func (sparseMatrix *SparseMatrix) GetValue(i int, j int) float64 {
  var lol ListOfList
  for _,lol = range sparseMatrix.cells {
    if LessThan(lol,i,j) {
      continue
    }
    if Equal(lol, i ,j){
      return lol.Value
    }
    return 0.0
  }
  return 0.0
}

func (sparseMatrix *SparseMatrix) SetValue(i int, j int, value float64) {
  var lol ListOfList
  var index int
  for index, lol = range sparseMatrix.cells {
    if LessThan(lol, i, j) {
      continue
    }
    if Equal(lol, i, j) {
      sparseMatrix.cells[index].Value = value
      return
    }
    sparseMatrix.cells = append(sparseMatrix.cells, ListOfList{})
    var k int
    for k = len(sparseMatrix.cells) - 2; k >= index; k-- {
      sparseMatrix.cells[k+1] = sparseMatrix.cells[k]
    }
    sparseMatrix.cells[index] = ListOfList{
      Row: i,
      Column: j,
      Value: value,
    }
    return
  }
  sparseMatrix.cells = append(sparseMatrix.cells, ListOfList{
    Row: i,
    Column: j,
    Value: value,
  })
}

func NewSparseMatrix(m int, n int) *SparseMatrix {
  return &SparseMatrix{
    cells: []ListOfList{},
    shape: [2]int{m, n},
  }
}

func main() {
  var sparseMatrix *SparseMatrix
  sparseMatrix = NewSparseMatrix(3, 3)
  sparseMatrix.SetValue(1, 1, 2.0)
  sparseMatrix.SetValue(1, 3, 3.0)
  fmt.Println(sparseMatrix)
  fmt.Println(sparseMatrix.NumNonZero())
}
```

