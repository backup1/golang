# Power

```go
func power(exponent int, index int) int {
  var power int = 1
  for index > 0 {
    if index&1 != 0 {
      power *= exponent
    }
    index >>= 1
    exponent *= exponent
  }
  return power
}
```

