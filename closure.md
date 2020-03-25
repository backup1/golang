# Closure

```go
func adder() func(int) int {
  sum := 0
  return func(x int) int {
    sum += x
    return sum
  }
}
func main() {
  // when we call "adder()",it returns the closure
  sumClosure := adder() // the value of the sum variable is 0
  sumClosure(1) //now the value of the sum variable is 0+1 = 1
  sumClosure(2) //now the value of the sum variable is 1+2=3
  //Use the value received from the closure somehow
}
```



