# Social Graph

```go
package main

import "fmt"

type SocialGraph struct {
  Size int
  Links [][]Link
}

type Link struct {
  Vertex1 int
  Vertex2 int
  LinkWeight int
}

func NewSocialGraph(num int) *SocialGraph {
  return &SocialGraph{
    Size : num,
    Links : make([][]Link,num),
  }
}

func (socialGraph *SocialGraph) AddLink(vertex1 int, vertex2 int, weight int) {
  socialGraph.Links[vertex1] = append(socialGraph.Links[vertex1], Link{Vertex1: vertex1, Vertex2: vertex2, LinkWeight: weight})
}

func (socialGraph *SocialGraph) PrintLinks() {
  var vertex int = 0
  fmt.Printf("Printing all links from %d\n",vertex)
  var link Link
  for _,link = range socialGraph.Links[vertex] {
    fmt.Printf("Link: %d -> %d (%d)\n",link.Vertex1,link.Vertex2,link.LinkWeight)
  }
  fmt.Println("Printing all links in graph.")
  var adjacent []Link
  for _,adjacent = range socialGraph.Links {
    for _,link = range adjacent {
      fmt.Printf("Link: %d -> %d (%d)\n",link.Vertex1,link.Vertex2,link.LinkWeight)
    }
  }
}

func main() {
  var socialGraph *SocialGraph = NewSocialGraph(4)
  socialGraph.AddLink(0, 1, 1)
  socialGraph.AddLink(0, 2, 1)
  socialGraph.AddLink(1, 3, 1)
  socialGraph.AddLink(2, 4, 1)
  socialGraph.PrintLinks()
}
```

Unit Test

```bash
$ ls
socialgraph.go  socialgraph_test.go

$ go test -run NewSocialGraph -v
=== RUN   TestNewSocialGraph
--- PASS: TestNewSocialGraph (0.00s)
PASS
ok      _/C_/cygwin64/home/djiang/golang/socialgraph    0.073s
```

```go
package main

import "testing"

func TestNewSocialGraph(test *testing.T) {
  var socialGraph *SocialGraph = NewSocialGraph(1)
  if socialGraph == nil {
    test.Errorf("error in creating a social Graph")
  }
}
```

```go
package main

import "fmt"

type Name string

type SocialGraph struct {
  GraphNodes map[Name]struct{}
  Links map[Name]map[Name]struct{}
}

func NewSocialGraph() *SocialGraph {
  return &SocialGraph{
    GraphNodes: make(map[Name]struct{}),
    Links: make(map[Name]map[Name]struct{}),
  }
}

func (socialGraph *SocialGraph) AddEntity(name Name) bool {
  var exists bool
  if _,exists = socialGraph.GraphNodes[name]; exists {
    return true
  }
  socialGraph.GraphNodes[name] = struct{}{}
  return true
}

func (socialGraph *SocialGraph) AddLink(name1 Name, name2 Name) {
  var exists bool
  if _,exists = socialGraph.GraphNodes[name1]; !exists {
    socialGraph.AddEntity(name1)
  }
  if _,exists = socialGraph.GraphNodes[name2]; !exists {
    socialGraph.AddEntity(name2)
  }
  if _,exists = socialGraph.Links[name1]; !exists {
    socialGraph.Links[name1] = make(map[Name]struct{})
  }
  socialGraph.Links[name1][name2] = struct{}{}
}

func (socialGraph *SocialGraph) PrintLinks() {
  var root Name = Name("Root")
  fmt.Printf("Printing all links adjacent to %s\n", root)
  var node Name
  for node = range socialGraph.Links[root] {
    // Edge exists from u to v.
    fmt.Printf("Link: %s -> %s\n", root, node)
  }
  var m map[Name]struct{}
  fmt.Println("Printing all links.")
  for root, m = range socialGraph.Links {
    var vertex Name
    for vertex = range m {
      // Edge exists from u to v.
      fmt.Printf("Link: %s -> %s\n", root, vertex)
    }
  }
}

func main() {
  var socialGraph *SocialGraph = NewSocialGraph()
  var root Name = Name("Root")
  var john Name = Name("John Smith")
  var per Name = Name("Per Jambeck")
  var cynthia Name = Name("Cynthia Gibas")
  socialGraph.AddEntity(root)
  socialGraph.AddEntity(john)
  socialGraph.AddEntity(per)
  socialGraph.AddEntity(cynthia)
  socialGraph.AddLink(root, john)
  socialGraph.AddLink(root, per)
  socialGraph.AddLink(root, cynthia)
  var mayo Name = Name("Mayo Smith")
  var lorrie Name = Name("Lorrie Jambeck")
  var ellie Name = Name("Ellie Vlocksen")
  socialGraph.AddLink(john, mayo)
  socialGraph.AddLink(john, lorrie)
  socialGraph.AddLink(per, ellie)
  socialGraph.PrintLinks()
}
```

