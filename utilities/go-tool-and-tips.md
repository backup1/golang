# Go Tool and Tips

The Go tool compiler can be invoked with the following command:

```bash
$ go build -gcflags="-S -N"   
```

The list options command syntax is as follows:

```bash
$ go build -x   
```

To test the race conditions, you can use the following command:

```bash
$ go test -race   
```

Running a test method by name can be done using the following syntax:

```bash
$ go test -run=method1   
```

To update your version of Go, you can use the following command:

```bash
$ go get -u   
```

Copying can be done with the following command:

```bash
$ go get -d   
```

To get depths, you can use the following command:

```bash
$ go get -t  
```

To get a list of software, you can use the following command:

```bash
$ go list -f 
```

The **GOROOT** variable can be configured as an environment variable with this command:

```bash
$ export GOROOT=/opt/go1.7.1
```

The **PATH** variable can be configured as an environment variable with this command:

```bash
$ export PATH=$GOROOT/bin:$PATH
```

The **GOPATH** variable can be configured as an environment variable with this command:

```bash
$ export GOPATH=$HOME/go
```

The **GOPATH** variable can be configured in the **PATH** variable with this command:

```bash
$ export PATH=$GOPATH/bin:$PATH
```

You can import packages with the following statements. Here, we show three different syntactical options:

```go
import "fmt"
import ft "fmt"
import . "fmt"
```

