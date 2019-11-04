# Mark-and-sweep algorithm

 The **mark-and-sweep algorithm** is based on an idea that was proposed by Dijkstra in 1978.

```go
func Mark( root *object){
  var markedAlready bool = IfMarked(root)
  if !markedAlready {
    map[root] = true
  }
  var references *object[] = GetReferences(root)
  var reference *object
  for _, reference = range references {
    Mark(reference)
  }
}

func Sweep(){
  var objects *[]object = GetObjects()
  var object *object
  for _, object = range objects {
    var markedAlready bool = IfMarked(object)
    if markedAlready {
      map[object] = true
    }
    Release(object)
  }
}
```

