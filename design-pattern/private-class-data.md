# Private Class Data

```go
package main

import (
  "encoding/json"
  "fmt"
)

type AccountDetails struct {
  id string
  accountType string
}

type Account struct {
  details *AccountDetails
  CustomerName string
}

func (account *Account) setDetails(id string,accountType string) {
  account.details = &AccountDetails{id,accountType}
}

func (account *Account) getId() string {
  return account.details.id
}

func (account *Account) getAccountType() string {
  return account.details.accountType
}

func main() {
  var account *Account = &Account{CustomerName: "John Jack"}
  account.setDetails("1234","current")
  jsonAccount,_ := json.Marshal(account)
  fmt.Println("Private Class hidden",string(jsonAccount))
  fmt.Println("Account Id",account.getId())
  fmt.Println("Account Type",account.getAccountType())
}
```

