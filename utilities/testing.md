# Testing

Test table

```bash
$ ls
testtable_test.go

$ go test -run TestAddition -v
=== RUN   TestAddition
--- FAIL: TestAddition (0.00s)
    testtable_test.go:17: 3 + 2 = 5, expected 1
FAIL
exit status 1
FAIL    _/C_/cygwin64/home/djiang/golang/testtable      0.072s
```

```go
package main

import "testing"

func TestAddition(test *testing.T) {
  cases := []struct{ integer1 , integer2 , resultSum int }{
    {1, 1, 2},
    {1, -1, 0},
    {1, 0, 1},
    {0, 0, 0},
    {3, 2, 1},
  }
  for _, cas := range cases {
    var sum int = cas.integer1 + cas.integer2
    var expected int = cas.resultSum
    if sum != expected {
      test.Errorf("%d + %d = %d, expected %d", cas.integer1, cas.integer2, sum, expected)
    }
  }
}
```

