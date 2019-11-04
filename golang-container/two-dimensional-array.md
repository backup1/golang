# Two-dimensional Array / Matrix

```go
package main

import "fmt"

func main() {
  var arr = [4][5]int{
    {4,5,7,8,9},
    {1,2,4,5,6},
    {9,10,11,12,14},
    {3,4,6,8,9},
  }

  fmt.Print(arr)
  fmt.Println()

  var value int = arr[2][3]

  fmt.Print(value)
}
```

Row Matrix and Column Matrix

```go
package main

import "fmt"

func main() {
  var rowMatrix = [1][3]int{
    {1,2,3},
  }
  fmt.Print(rowMatrix)
  fmt.Println()
  var colMatrix = [4][1]int{
    {1},
    {2},
    {3},
    {4},
  }
  fmt.Print(colMatrix)
}
```

Lower / Upper Matrix and Nul / Identity Matrix

```go
package main

import "fmt"

func Identity(order int) [][]float64 {
  var matrix [][]float64 = make([][]float64,order)
  var i int
  for i = 0; i < order; i++ {
    var temp []float64 = make([]float64,order)
    temp[i] = 1
    matrix[i] = temp
  }
  return matrix
}

func main() {
  var lowermatrix = [3][3]int{
    {1,0,0},
    {1,1,0},
    {2,1,1},
  }
  fmt.Println(lowermatrix)
  var uppermatrix = [3][3]int{
    {1,2,3},
    {0,1,4},
    {0,0,1},
  }
  fmt.Println(uppermatrix)
  var nulmatrix = [3][3]int{
    {0,0,0},
    {0,0,0},
    {0,0,0},
  }
  fmt.Println(nulmatrix)
  fmt.Println(Identity(4))
}
```

2 x 2 matrix

```go
package main

import "fmt"

func add(matrix1 [2][2]int,matrix2 [2][2]int) [2][2]int {
  var l,m int
  var sum [2][2]int
  for l = 0; l < 2; l++ {
    for m = 0; m < 2; m++ {
      sum[l][m] = matrix1[l][m] + matrix2[l][m]
    }
  }
  return sum
}

func subtract(matrix1 [2][2]int,matrix2 [2][2]int) [2][2]int {
  var l,m int
  var diff [2][2]int
  for l = 0; l < 2; l++ {
    for m = 0; m < 2; m++ {
      diff[l][m] = matrix1[l][m] - matrix2[l][m]
    }
  }
  return diff
}

func multiply(matrix1 [2][2]int,matrix2 [2][2]int) [2][2]int {
  var l,m,n int
  var prod [2][2]int
  for l = 0; l < 2; l++ {
    for m = 0; m < 2; m++ {
      prod[l][m] = 0
      for n = 0; n < 2; n++ {
        prod[l][m] += matrix1[l][n]*matrix2[n][m]
      }
    }
  }
  return prod
}

func transpose(matrix [2][2]int) [2][2]int {
  var l,m int
  var trans [2][2]int
  for l = 0; l < 2; l++ {
    for m = 0; m < 2; m++ {
      trans[l][m] = matrix[m][l]
    }
  }
  return trans
}

func determinant(matrix [2][2]int) float64 {
  var det int = matrix[0][0]*matrix[1][1] - matrix[0][1]*matrix[1][0]
  return float64(det)
}

func inverse(matrix [2][2]int) [][]float64 {
  var det float64 = determinant(matrix)
  var inv [][]float64
  inv[0][0] = float64(matrix[1][1])/det
  inv[0][1] = float64(-matrix[0][1])/det
  inv[1][0] = float64(-matrix[1][0])/det
  inv[1][1] = float64(matrix[0][0])/det
  return inv
}

func main() {
  var matrix1 = [2][2]int{
    {4,5},
    {1,2},
  }
  var matrix2 = [2][2]int{
    {6,7},
    {3,4},
  }
  var sum [2][2]int = add(matrix1,matrix2)
  fmt.Println(sum)
  var diff [2][2]int = subtract(matrix1,matrix2)
  fmt.Println(diff)
  var prod [2][2]int = multiply(matrix1,matrix2)
  fmt.Println(prod)
}
```

ZigZag matrix

```go
package main

import "fmt"

func PrintZigZag(n int) []int {
  var zigzag []int = make([]int,n*n)
  var i int = 0
  var m int = 2*n
  var p int
  for p = 1; p <= m; p++ {
    var x int = p-n
    if x < 0 {
      x = 0
    }
    var y int = p-1
    if y > n-1 {
      y = n-1
    }
    var j int = m-p
    if j > p {
      j = p
    }
    var k int
    for k = 0; k < j; k++ {
      if p%2 == 0 {
        zigzag[(x+k)*n+y-k] = i
      } else {
        zigzag[(y-k)*n+x+k] = i
      }
      i++
    }
  }
  return zigzag
}

func main() {
  var n int = 5
  var length int = 2
  var i,sketch int
  for i,sketch = range PrintZigZag(n) {
    fmt.Printf("%*d ",length,sketch)
    if i%n == n-1 {
      fmt.Println()
    }
  }
}
```

Spiral Matrix

```go
package main

import "fmt"

func PrintSpiral(n int) []int {
  var left int = 0
  var top int = 0
  var right int = n-1
  var bottom int = n-1
  var size int = n*n
  var s []int = make([]int,size)
  var i int = 0
  for left < right {
    var c int
    for c = left; c <= right; c++ {
      s[top*n+c] = i
      i++
    }
    top++
    var r int
    for r = top; r <= bottom; r++ {
      s[r*n+right] = i
      i++
    }
    right--
    if top == bottom {
      break
    }
    for c = right; c >= left; c-- {
      s[bottom*n+c] = i
      i++
    }
    bottom--
    for r = bottom; r >= top; r-- {
      s[r*n+left] = i
      i++
    }
    left++
  }
  s[top*n+left] = i
  return s
}

func main() {
  var n int = 5
  var length int = 2
  var i,sketch int
  for i,sketch = range PrintSpiral(n) {
    fmt.Printf("%*d ",length,sketch)
    if i%n == n-1 {
      fmt.Println()
    }
  }
}
```

Boolean Matrix

```go
package main

import "fmt"

func change(matrix [3][3]int) [3][3]int {
  var i,j int
  var rows,cols [3]int
  var ret [3][3]int
  for i = 0; i < 3; i++ {
    for j = 0; j < 3; j++ {
      if matrix[i][j] == 1 {
        rows[i] = 1
        cols[j] = 1
      }
    }
  }
  for i = 0; i < 3; i++ {
    for j = 0; j < 3; j++ {
      if rows[i] == 1 || cols[j] == 1 {
        ret[i][j] = 1
      }
    }
  }
  return ret
}

func print(matrix [3][3]int) {
  var i,j int
  for i = 0; i < 3; i++ {
    for j = 0; j < 3; j++ {
      fmt.Printf("%d",matrix[i][j])
    }
    fmt.Printf("\n")
  }
}

func main() {
  var matrix = [3][3]int{{1,0,0},{0,0,0},{0,0,0}}
  print(matrix)
  matrix = change(matrix)
  print(matrix)
}
```

