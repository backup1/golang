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
export GOPATH=$HOME/golang
export TMPDIR=$HOME/tmp
```

