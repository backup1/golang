# Sort

```go
package main

import (
  "fmt"
  "sort"
)

type Employee struct {
  Name string
  ID string
  SSN int
  Age int
}

func (employee Employee) ToString() string {
  return fmt.Sprintf("%s: %d,%s,%d",employee.Name,employee.Age,employee.ID,employee.SSN)
}

type SortByAge []Employee

func (sortIntf SortByAge) Len() int {
  return len(sortIntf)
}
func (sortIntf SortByAge) Swap(i int,j int) {
  sortIntf[i],sortIntf[j] = sortIntf[j],sortIntf[i]
}
func (sortIntf SortByAge) Less(i int,j int) bool {
  return sortIntf[i].Age < sortIntf[j].Age
}

func main() {
  var employees = []Employee{
    {"Graham","231",235643,31},
    {"John", "3434",245643,42},
    {"Michael","8934",32432, 17},
    {"Jenny", "24334",32444,26},
  }
  fmt.Println(employees)
  sort.Sort(SortByAge(employees))
  fmt.Println(employees)
  sort.Slice(employees, func(i int,j int) bool {
    return employees[i].Age > employees[j].Age
  })
  fmt.Println(employees)
}
```

```go
package main

import (
  "fmt"
  "sort"
)

type Mass float64
type Miles float64

type Thing struct {
  name string
  mass Mass
  distance Miles
  meltingpoint int
  freezingpoint int
}

type ByFactor func(thing1 *Thing,thing2 *Thing) bool

func (byFactor ByFactor) Sort(things []Thing) {
  var sortedThings *ThingSorter = &ThingSorter{
    things: things,
    byFactor: byFactor,
  }
  sort.Sort(sortedThings)
}

type ThingSorter struct {
  things []Thing
  byFactor func(thing1 *Thing,thing2 *Thing) bool
}

func (thingSorter *ThingSorter) Len() int {
  return len(thingSorter.things)
}

func (thingSorter *ThingSorter) Swap(i int,j int) {
  thingSorter.things[i],thingSorter.things[j] = thingSorter.things[j],thingSorter.things[i]
}

func (thingSorter *ThingSorter) Less(i int,j int) bool {
  return thingSorter.byFactor(&thingSorter.things[i],&thingSorter.things[j])
}

func main() {
  var Things = []Thing{
    {"IronRod", 0.055, 0.4, 3000, -180},
    {"SteelChair", 0.815, 0.7, 4000, -209},
    {"CopperBowl", 1.0, 1.0, 60, -30},
    {"BrassPot", 0.107, 1.5, 10000, -456},
  }

  var name func(*Thing,*Thing) bool = func(p1 *Thing,p2 *Thing) bool {
    return p1.name < p2.name
  }
  var mass func(*Thing,*Thing) bool = func(p1 *Thing,p2 *Thing) bool {
    return p1.mass < p2.mass
  }
  var distance func(*Thing,*Thing) bool = func(p1 *Thing,p2 *Thing) bool {
    return p1.distance < p2.distance
  }
  var decreasingDistance func(*Thing,*Thing) bool = func(p1,p2 *Thing) bool {
    return distance(p2, p1)
  }

  ByFactor(name).Sort(Things)
  fmt.Println("By name:", Things)
  ByFactor(mass).Sort(Things)
  fmt.Println("By mass:", Things)
  ByFactor(distance).Sort(Things)
  fmt.Println("By distance:", Things)
  ByFactor(decreasingDistance).Sort(Things)
  fmt.Println("By decreasing distance:", Things)
}
```

```go
package main

import (
  "fmt"
  "sort"
)

type Commit struct {
  username string
  lang string
  numlines int
}

type LessFunc func(p1 *Commit,p2 *Commit) bool

type MultiSorter struct {
  commits []Commit
  lessFunction []LessFunc
}

func (multiSorter *MultiSorter) Sort(commits []Commit) {
  multiSorter.commits = commits
  sort.Sort(multiSorter)
}

func OrderedBy(lessFunction ...LessFunc) *MultiSorter {
  return &MultiSorter {
    lessFunction: lessFunction,
  }
}

func (multiSorter *MultiSorter) Len() int {
  return len(multiSorter.commits)
}

func (multiSorter *MultiSorter) Swap(i int,j int) {
  multiSorter.commits[i],multiSorter.commits[j] = multiSorter.commits[j],multiSorter.commits[i]
}

func (multiSorter *MultiSorter) Less(i int,j int) bool {
  var p *Commit = &multiSorter.commits[i]
  var q *Commit = &multiSorter.commits[j]
  var k int
  for k = 0; k < len(multiSorter.lessFunction)-1; k++ {
    less := multiSorter.lessFunction[k]
    switch {
    case less(p,q):
      return true
    case less(q,p):
      return false
    }
  }
  return multiSorter.lessFunction[k](p,q)
}

func main() {
  var Commits = []Commit{
    {"james", "Javascript", 110},
    {"ritchie", "python", 250},
    {"fletcher", "Go", 300},
    {"ray", "Go", 400},
    {"john", "Go", 500},
    {"will", "Go", 600},
    {"dan", "C++", 500},
    {"sam", "Java", 650},
    {"hayvard", "Smalltalk", 180},
  }
  var user func(*Commit,*Commit) bool = func(c1 *Commit,c2 *Commit) bool {
    return c1.username < c2.username
  }
  var language func(*Commit,*Commit) bool = func(c1 *Commit,c2 *Commit) bool {
    return c1.lang < c2.lang
  }
  var increasingLines func(*Commit,*Commit) bool = func(c1 *Commit,c2 *Commit) bool {
    return c1.numlines < c2.numlines
  }
  var decreasingLines func(*Commit,*Commit) bool = func(c1 *Commit,c2 *Commit) bool {
    return c1.numlines > c2.numlines // Note: > orders downwards.
  }
  OrderedBy(user).Sort(Commits)
  fmt.Println("By username:",Commits)
  OrderedBy(user,increasingLines).Sort(Commits)
  fmt.Println("By username,asc order",Commits)
  OrderedBy(user,decreasingLines).Sort(Commits)
  fmt.Println("By username,desc order",Commits)
  OrderedBy(language,increasingLines).Sort(Commits)
  fmt.Println("By lang,asc order",Commits)
  OrderedBy(language,decreasingLines,user).Sort(Commits)
  fmt.Println("By lang,desc order",Commits)
}
```

