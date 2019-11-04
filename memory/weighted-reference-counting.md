# Weighted Reference Counting

```go
type ReferenceCounter struct {
  num *uint32
  pool *sync.Pool
  removed *uint32
  weight int
}

func WeightedReference() int {
  var references []ReferenceCounter = GetReferences(root)
  var reference ReferenceCounter
  var sum int
  for _, reference = range references {
    sum += reference.weight
  }
  return sum
}
```

