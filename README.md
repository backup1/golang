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

```bash
$ go mod init example.com/hello
$ go list -m all
$ go list -m -versions rsc.io/sampler
$ go get rsc.io/sampler@v1.3.1
$ go list -m rsc.io/q...
$ go mod tidy
$ go mod why -m rsc.io/binaryregexp
$ sudo go build ./...
$ sudo go test ./...
$ git tag v1.2.0
$ git push origin v1.2.0
```

Publish a module

```go
$ export GO111MODULE=on
$ go mod init
$ go mod vendor # if you have vendor/ folder, will automatically integrate
$ go build
```

```bash
$ go mod tidy
$ go test ./...
ok      example.com/hello       0.015s
$ git add go.mod go.sum hello.go hello_test.go
$ git commit -m "hello: changes for v0.1.0"
$ git tag v0.1.0
$ git push origin v0.1.0
```

testing local changes with go.mod

Git init

```go
module github.com/acme/foo

go 1.12

require (
	github.com/acme/bar v1.0.0
)

replace github.com/acme/bar => /path/to/local/bar
```

```bash
$ git config -l
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

```bash
$ go mod edit -replace github.com/acme/bar=/path/to/local/bar
```

