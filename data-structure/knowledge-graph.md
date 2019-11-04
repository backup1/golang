# Knowledge Graph

```go
package main

import "fmt"

type Class struct {
  Name string
}

type KnowledgeGraph struct {
  GraphNodes map[Class]struct{}
  Links map[Class]map[Class]struct{}
}

func NewKnowledgeGraph() *KnowledgeGraph {
  return &KnowledgeGraph{
    GraphNodes: make(map[Class]struct{}),
    Links: make(map[Class]map[Class]struct{}),
  }
}

func (knowledgeGraph *KnowledgeGraph) AddClass(class Class) {
  var exists bool
  if _,exists = knowledgeGraph.GraphNodes[class]; !exists {
    knowledgeGraph.GraphNodes[class] = struct{}{}
  }
}

func (knowledgeGraph *KnowledgeGraph) AddLink(class1 Class, class2 Class) {
  var exists bool
  if _, exists = knowledgeGraph.GraphNodes[class1]; !exists {
    knowledgeGraph.AddClass(class1)
  }
  if _, exists = knowledgeGraph.GraphNodes[class2]; !exists {
    knowledgeGraph.AddClass(class2)
  }
  if _, exists = knowledgeGraph.Links[class1]; !exists {
    knowledgeGraph.Links[class1] = make(map[Class]struct{})
  }
  knowledgeGraph.Links[class1][class2] = struct{}{}
}

func (knowledgeGraph *KnowledgeGraph) PrintLinks() {
  var car Class = Class{"Car"}
  fmt.Printf("Printing all links adjacent to %s\n", car.Name)
  var node Class
  for node = range knowledgeGraph.Links[car] {
    fmt.Printf("Link: %s -> %s\n", car.Name, node.Name)
  }
  var m map[Class]struct{}
  fmt.Println("Printing all links.")
  for car, m = range knowledgeGraph.Links {
    var vertex Class
    for vertex = range m {
      fmt.Printf("Link: %s -> %s\n", car.Name, vertex.Name)
    }
  }
}

func main() {
  var knowledgeGraph *KnowledgeGraph = NewKnowledgeGraph()
  var car = Class{"Car"}
  var tyre = Class{"Tyre"}
  var door = Class{"Door"}
  var hood = Class{"Hood"}
  knowledgeGraph.AddClass(car)
  knowledgeGraph.AddClass(tyre)
  knowledgeGraph.AddClass(door)
  knowledgeGraph.AddClass(hood)
  knowledgeGraph.AddLink(car, tyre)
  knowledgeGraph.AddLink(car, door)
  knowledgeGraph.AddLink(car, hood)
  var tube = Class{"Tube"}
  var axle = Class{"Axle"}
  var handle = Class{"Handle"}
  var windowGlass = Class{"Window Glass"}
  knowledgeGraph.AddClass(tube)
  knowledgeGraph.AddClass(axle)
  knowledgeGraph.AddClass(handle)
  knowledgeGraph.AddClass(windowGlass)
  knowledgeGraph.AddLink(tyre, tube)
  knowledgeGraph.AddLink(tyre, axle)
  knowledgeGraph.AddLink(door, handle)
  knowledgeGraph.AddLink(door, windowGlass)
  knowledgeGraph.PrintLinks()
}
```

Unit Test

```bash
$ ls
knowledgegraph.go  knowledgegraph_test.go

$ go test -run NewKnowledgeGraph -v
=== RUN   TestNewKnowledgeGraph
--- PASS: TestNewKnowledgeGraph (0.00s)
    knowledgegraph_test.go:7: &{map[] map[]}
PASS
ok      _/C_/cygwin64/home/djiang/golang/knowledgegraph 2.066s

$ go test
PASS
ok      _/C_/cygwin64/home/djiang/golang/knowledgegraph 0.069s
```

```go
package main

import "testing"

func TestNewKnowledgeGraph(test *testing.T) {
  var knowledgeGraph *KnowledgeGraph = NewKnowledgeGraph()
  test.Log(knowledgeGraph)
  if knowledgeGraph == nil {
    test.Errorf("error in creating a knowledgeGraph")
  }
}
```

