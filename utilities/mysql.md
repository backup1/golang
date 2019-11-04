# MySql

You need to install mysql as well mysql driver \(for golang\)

```bash
$ go get -u github.com/go-sql-driver/mysql
```

```go
package main

import (
  "fmt"
  "database/sql"
  _ "github.com/go-sql-driver/mysql"
)

type Customer struct {
  CustomerId int
  CustomerName string
  SSN string
}

func GetConnection() (database *sql.DB) {
  databaseDriver := "mysql"
  databaseUser := "newuser"
  databasePass := "newuser"
  databaseName := "crm"
  database,err := sql.Open(databaseDriver, databaseUser+":"+databasePass+"@/"+databaseName)
  if err != nil {
    panic(err.Error())
  }
  return database
}

func GetCustomers() []Customer {
  var database *sql.DB
  database = GetConnection()
  var err error
  var rows *sql.Rows
  rows,err = database.Query("SELECT * FROM Customer ORDER BY Customerid DESC")
  if err != nil {
    panic(err.Error())
  }
  var customer Customer
  customer = Customer{}
  var customers []Customer
  customers = []Customer{}
  for rows.Next() {
    var customerId int
    var customerName string
    var ssn string
    err = rows.Scan(&customerId, &customerName, &ssn)
    if err != nil {
      panic(err.Error())
    }
    customer.CustomerId = customerId
    customer.CustomerName = customerName
    customer.SSN = ssn
    customers = append(customers, customer)
  }
  defer database.Close()
  return customers
}

func InsertCustomer(customer Customer) {
  var database *sql.DB
  database = GetConnection()
  var err error
  var insert *sql.Stmt
  insert,err = database.Prepare("INSERT INTO CUSTOMER(CustomerName,SSN) VALUES(?,?)")
  if err != nil {
    panic(err.Error())
  }
  insert.Exec(customer.CustomerName,customer.SSN)
  defer database.Close()
}

func UpdateCustomer(customer Customer){
  var database *sql.DB
  database = GetConnection()
  var err error
  var update *sql.Stmt
  update,err = database.Prepare("UPDATE CUSTOMER SET CustomerName=?, SSN=? WHERE CustomerId=?")
  if err != nil {
    panic(err.Error())
  }
  update.Exec(customer.CustomerName,customer.SSN,customer.CustomerId)
  defer database.Close()
}

func deleteCustomer(customer Customer){
  var database *sql.DB
  database = GetConnection()
  var err error
  var delete *sql.Stmt
  delete,err = database.Prepare("DELETE FROM Customer WHERE Customerid=?")
  if err != nil {
    panic(err.Error())
  }
  delete.Exec(customer.CustomerId)
  defer database.Close()
}

func main() {
  var customers []Customer
  customers = GetCustomers()
  fmt.Println("Before Insert",customers)
  var customer1 Customer
  customer1.CustomerName = "Arnie Smith"
  customer1.SSN = "2386343"
  InsertCustomer(customer1)
  customers = GetCustomers()
  fmt.Println("After Insert",customers)

  fmt.Println("Before Update",customers)
  var customer2 Customer
  customer2.CustomerName = "George Thompson"
  customer2.SSN = "23233432"
  customer2.CustomerId = 5
  UpdateCustomer(customer2)
  customers = GetCustomers()
  fmt.Println("After Update",customers)

  fmt.Println("Before Delete",customers)
  var customer3 Customer
  customer3.CustomerName = "George Thompson"
  customer3.SSN = "23233432"
  customer3.CustomerId = 5
  deleteCustomer(customer3)
  customers = GetCustomers()
  fmt.Println("After Delete",customers)
}
```

View.tmpl

```markup
{{ define "View" }}
  {{ template "Header" }}
  {{ template "Menu"  }}
  <br>
  <h1>View Customer</h1>
  <br>
  <br>
  <table border="1">
  <tr>
    <td>CustomerId</td>
    <td>CustomerName</td>
    <td>SSN</td>
    <td>Update</td>
    <td>Delete</td>
  </tr>
  {{ if . }}
    {{ range . }}
    <tr>
      <td>{{ .CustomerId }}</td>
      <td>{{ .CustomerName }}</td>
      <td>{{ .SSN }}</td>
      <td><a href="/delete?id={{.CustomerId}}" onclick="return confirm('Are you sure you want to delete?');">Delete</a> </td>
      <td><a href="/update?id={{.CustomerId}}">Update</a> </td>
    </tr>
    {{ end }}
  {{ end }}
  </table>
  {{ template "Footer" }}
{{ end }}
```

