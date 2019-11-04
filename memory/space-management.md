# Space Management

Pass by value

```go
package main

import "fmt"

func addOne(num int) {
  num++
  fmt.Println("added to num",num,"Address of num",&num)
}

func main() {
  var number int = 17
  fmt.Println("value of number", number, "Address of number", &number)
  addOne(number)
  fmt.Println("value of number after adding One", number, "Address of", &number)
}
```

Pass by pointer

```go
package main

import "fmt"

func addOne(num *int) {
  *num++
  fmt.Println("added to num",num,"Address of num",&num,"Value Points To",*num)
}

func main() {
  var number int = 17
  fmt.Println("value of number", number, "Address of number", &number)
  addOne(&number)
  fmt.Println("value of number after adding One", number, "Address of", &number)
}
```

