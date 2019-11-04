# Profiling

**Profiling** in Go can be enabled by using the **cpuprofile** and **memprofile** flags. The Go testing package has support for benchmarking and profiling. The cpuprofile flag can be invoked by the following command:

```bash
$ go test -run=none -bench=ClientServerParallel4 -cpuprofile=cprofile net/http
```

The benchmark can be written to a **cprofile** output file using the following command:

```bash
$ go tool pprof --text http.test cprof
```

Let's look at an example of how to profile the programs that you have written. The **flag.Parse** method reads the command-line flags. The CPU profiling output is written to a file. The **StopCPUProfile** method on the profiler is called to flush any pending file output that needs to be written before the program stops:

```go
var profile = flag.String("cpuprofile", "", "cpu profile to output file")
func main() {
  flag.Parse()
  if *profile != "" {
    var file *os.File
    var err error
    file, err = os.Create(*profile)
    if err != nil {
      log.Fatal(err)
    }
    pprof.StartCPUProfile(file)
    defer pprof.StopCPUProfile()
  }
}
```

