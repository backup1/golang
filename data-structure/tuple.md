# Tuple

```go
package main

import "fmt"

func powers(a int) (int,int,error) {
  square := a*a
  cube := square*a
  return square,cube,nil
}

func main(){
  var sq,cube int
  sq,cube,_ = powers(3)
  fmt.Println("Square",sq,"Cube",cube)
}
```

```go
package main

import "fmt"

func h(x int,y int) int {
  return x*y
}

func g(l int,m int) (x int,y int) {
  x = 2*l
  y = 4*m
  return
}

func main() {
  fmt.Println(h(g(1,2)))
}
```

