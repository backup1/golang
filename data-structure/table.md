# Table

```go
package main

import "fmt"

type Table struct {
  rows []Row
  name string
  columnNames []string
}

type Row struct {
  columns []Column
  id int
}

type Column struct {
  id int
  value string
}

func printTable(table Table) {
  var rows []Row = table.rows
  fmt.Println(table.name)
  for _,row := range rows {
    var columns []Column = row.columns
    for i,column := range columns {
      fmt.Println(table.columnNames[i],column.id,column.value)
    }
  }
}

func main() {
  var table Table = Table{}
  table.name = "Customer"
  table.columnNames = []string{"Id", "Name","SSN"}
  var rows []Row = make([]Row,2)
  rows[0] = Row{}
  var columns1 []Column = make([]Column,3)
  columns1[0] = Column{1,"323"}
  columns1[1] = Column{1,"John Smith"}
  columns1[2] = Column{1,"3453223"}
  rows[0].columns = columns1
  rows[1] = Row{}
  var columns2 []Column = make([]Column,3)
  columns2[0] = Column{2,"223"}
  columns2[1] = Column{2,"Curran Smith"}
  columns2[2] = Column{2,"3223211"}
  rows[1].columns = columns2
  table.rows = rows
  fmt.Println(table)
  printTable(table)
}
```

