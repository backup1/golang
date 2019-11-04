# CRM - CRUD web form

The example will not work if there is a firewall installed on your machine. You need to check with your network admin to allow its running.

```go
package main

import (
  "net/http"
  "text/template"
  "log"
)

func Home(writer http.ResponseWriter,reader *http.Request) {
  var template_html *template.Template
  template_html = template.Must(template.ParseFiles("main.html"))
  template_html.Execute(writer,nil)
}

func Create(writer http.ResponseWriter,request *http.Request) {
  template_html.ExecuteTemplate(writer,"Create",nil)
}

func Insert(writer http.ResponseWriter,request *http.Request) {
  var customer Customer
  customer.CustomerName = request.FormValue("customername")
  customer.SSN = request.FormValue("ssn")
  InsertCustomer(customer)
  var customers []Customer
  customers = GetCustomers()
  template_html.ExecuteTemplate(writer,"Home",customers)
}

func Alter(writer http.ResponseWriter,request *http.Request) {
  var customer Customer
  var customerId int
  var customerIdStr string
  customerIdStr = request.FormValue("id")
  fmt.Sscanf(customerIdStr,"%d",&customerId)
  customer.CustomerId = customerId
  customer.CustomerName = request.FormValue("customername")
  customer.SSN = request.FormValue("ssn")
  UpdateCustomer(customer)
  var customers []Customer
  customers = GetCustomers()
  template_html.ExecuteTemplate(writer,"Home",customers)
}

func Update(writer http.ResponseWriter,request *http.Request) {
  var customerId int
  var customerIdStr string
  customerIdStr = request.FormValue("id")
  fmt.Sscanf(customerIdStr,"%d",&customerId)
  var customer Customer
  customer = GetCustomerById(customerId)
  template_html.ExecuteTemplate(writer,"Update",customer)
}

func Delete(writer http.ResponseWriter,request *http.Request) {
  var customerId int
  var customerIdStr string
  customerIdStr = request.FormValue("id")
  fmt.Sscanf(customerIdStr,"%d",&customerId)
  var customer Customer
  customer = GetCustomerById(customerId)
  DeleteCustomer(customer)
  var customers []Customer
  customers = GetCustomers()
  template_html.ExecuteTemplate(writer,"Home",customers)
}

func View(writer http.ResponseWriter,request *http.Request) {
  var customerId int
  var customerIdStr string
  customerIdStr = request.FormValue("id")
  fmt.Sscanf(customerIdStr,"%d",&customerId)
  var customer Customer
  customer = GetCustomerById(customerId)
  fmt.Println(customer)
  var customers []Customer
  customers= []Customer{customer}
  customers.append(customer)
  template_html.ExecuteTemplate(writer,"View",customers)
}

func main() {
  log.Println("Server started on: http://localhost:8000")
  http.HandleFunc("/",Home)
  http.HandleFunc("/alter", Alter)
  http.HandleFunc("/create", Create)
  http.HandleFunc("/update", Update)
  http.HandleFunc("/view", View)
  http.HandleFunc("/insert", Insert)
  http.HandleFunc("/delete", Delete)
  http.ListenAndServe(":8000",nil)
}
```

Header.tmpl

```markup
{{ define "Header" }}
<!DOCTYPE html>
<html>
  <head>
    <title>CRM</title>
    <meta charset="UTF-8" />
  </head>
  <body>
    <h1>Customer Management – CRM</h1>
{{ end }}
```

Footer.tmpl

```markup
{{ define "Footer" }}
  </body>
</html>
{{ end }}
```

Menu.tmpl

```markup
{{ define "Menu" }}
<a href="/">Home</a> | <a href="/create">Create Customer</a>
{{ end }}
```

Create.tmpl

```markup
{{ define "Create" }}
  {{ template "Header" }}
  {{ template "Menu"  }}
  <br>
  <h1>Create Customer</h1>
  <br>
  <br>
  <form method="post" action="/insert">
    Customer Name: <input type="text" name="customername" placeholder="customername" autofocus/>
    <br>
    <br>
    SSN: <input type="text" name="ssn" placeholder="ssn"/>
    <br>
    <br>
    <input type="submit" value="Create Customer"/>
  </form>
  {{ template "Footer" }}
{{ end }}
```

Update.tmpl

```markup
{{ define "Update" }}
  {{ template "Header" }}
  {{ template "Menu" }}
  <br>
  <h1>Update Customer</h1>
  <br>
  <br>
  <form method="post" action="/alter">
    <input type="hidden" name="id" value="{{ .CustomerId }}" />
    Customer Name: <input type="text" name="customername" placeholder="customername" value="{{ .CustomerName }}" autofocus>
    <br>
    <br>
    SSN: <input type="text" name="ssn" value="{{ .SSN }}" placeholder="ssn"/>
    <br>
    <br>
    <input type="submit" value="Update Customer"/>
  </form>
  {{ template "Footer" }}
{{ end }}
```

