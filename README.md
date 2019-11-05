# Introduction

Install golang : [https://golang.org/doc/install](%20https://golang.org/doc/install)

Install mysql driver

```bash
$ go get -u github.com/go-sql-driver/mysql
```

Install last golang on Ubuntu

```bash
$ sudo add-apt-repository ppa:longsleep/golang-backports
$ sudo apt-get update
$ sudo apt-get install golang-go
```

For a dedicated version

```bash
$ sudo add-apt-repository ppa:gophers/archive
$ sudo apt-get update
$ sudo apt-get install golang-1.11-go
```

Config specific for golang \(especially when you are not the root\)

```bash
$ cat ~/.zshenv.user 
... ...
export PATH=$PATH:$HOME/local/go/bin # optional
export GOPATH=$HOME/golang
export TMPDIR=$HOME/tmp
```

\[deprecated\] gopkg [https://golang.github.io/dep](https://golang.github.io/dep)

go.mod \[since 1.11\] [https://blog.golang.org/using-go-modules](https://blog.golang.org/using-go-modules)

This post introduced these workflows using Go modules:

* `go mod init` creates a new module, initializing the `go.mod` file that describes it.
* `go build`, `go test`, and other package-building commands add new dependencies to `go.mod` as needed.
* `go list -m all` prints the current module’s dependencies.
* `go get` changes the required version of a dependency \(or adds a new dependency\).
* `go mod tidy` removes unused dependencies.

```text
$ go mod init example.com/hello
$ go list -m all
$ go list -m -versions rsc.io/sampler
$ go get rsc.io/sampler@v1.3.1
$ go list -m rsc.io/q...
$ go mod tidy
```

