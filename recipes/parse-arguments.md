# Parse arguments / flags

```bash
$ ls
parseargs.go

$ go build -o test

$ ./test arg1 arg2
[C:\cygwin64\home\djiang\golang\testtable\test\test arg1 arg2]
The binary name is: C:\cygwin64\home\djiang\golang\testtable\test\test
[arg1 arg2]
Arg 0 = arg1
Arg 1 = arg2
```

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  args := os.Args
  fmt.Println(args)
  progName := args[0]
  fmt.Printf("The binary name is: %s\n",progName)
  otherArgs := args[1:]
  fmt.Println(otherArgs)
  for idx,arg := range otherArgs {
    fmt.Printf("Arg %d = %s\n",idx,arg)
  }
}
```

The Go package for flag handling does not support flag combining like ls -ll, where there are multiple flags after a single dash. Each flag must be separate. The Go flag package also does not differentiate between long options and short ones. Finally, -flag and --flag are equivalent.

```bash
$ ls
flags.go

$ go build -o util

$ ./util -retry 2 -prefix=example -array=1,2
example2019/10/31 Retrying connection
example2019/10/31 Sending array [1 2]
example2019/10/31 Retrying connection
example2019/10/31 Sending array [1 2]
```

```go
package main

import (
  "flag"
  "fmt"
  "log"
  "os"
  "strings"
)

// Custom type need to implement flag.Value interface
// to be able to use it in flag.Var function.
type ArrayValue []string

func (s *ArrayValue) String() string {
  return fmt.Sprintf("%v",*s)
}

func (a *ArrayValue) Set(s string) error {
  *a = strings.Split(s,",")
  return nil
}

func main() {
  retry := flag.Int("retry",-1,"Defines max retry count")
  var logPrefix string
  flag.StringVar(&logPrefix,"prefix","","Logger prefix")
  var arr ArrayValue
  flag.Var(&arr,"array","Input array to iterate through.")
  flag.Parse()
  logger := log.New(os.Stdout,logPrefix,log.Ldate)
  retryCount := 0
  for retryCount < *retry {
    logger.Println("Retrying connection")
    logger.Printf("Sending array %v\n",arr)
    retryCount++
  }
}
```

