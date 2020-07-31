# Build / Compilation

Build with vendor

```bash
go build -mod=vendor
```

Build with all dependencies \(huge size, but more portable\)

```bash
GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -mod vendor
```

Build with OS type and shrink the size

```bash
GOOS=linux; go build -ldflags="-s -w"
```

Go compilation option

[https://golang.org/pkg/net/](https://golang.org/pkg/net/)

```bash
export GODEBUG=netdns=go    # force pure Go resolver
export GODEBUG=netdns=cgo   # force cgo resolver
```

