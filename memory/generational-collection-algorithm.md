# Generational collection algorithm

```go
func GenerationCollect(){
  var currentGeneration int = 3
  var objects *[]object = GetObjectsFromOldGeneration(3)
  var object *object
  for _, object = range objects {
    var markedAlready bool = IfMarked(object)
    if markedAlready {
      map[object] = true
    }
  }
}
```

