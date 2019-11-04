# Error Management

Panic, defer, and recover are used to handle complex errors.

```go
package main

import(
  "fmt"
  "errors"
)

func FirstFunc(v interface{}) (interface{}, error) {
  var ok bool
  if !ok {
    return nil, errors.New("false error")
  }
  return v, nil
}

func SecondFunc() {
  defer func() {
    var err interface{}
    if err = recover(); err != nil {
      fmt.Println("recovering error", err)
    }
  }()
  var v interface{} = struct{}{}
  var err error
  if _, err = FirstFunc(v); err != nil {
    panic(err)
  }
  fmt.Println("The error never happen")
}

func main() {
  SecondFunc()
  fmt.Println("The execution ended")
}
```

It’s important to check for errors when closing a file, even in a deferred function.

[https://gobyexample.com/defer](https://gobyexample.com/defer)

```go
func main() {
  f := createFile("/tmp/defer.txt")
  defer closeFile(f)
  writeFile(f)
}

func closeFile(f *os.File) {
  fmt.Println("closing")
  err := f.Close()
  if err != nil {
    fmt.Fprintf(os.Stderr, "error: %v\n", err)
    os.Exit(1)
  }
}
```

