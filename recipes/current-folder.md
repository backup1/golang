# Current Folder / PID

```go
package main

import (
  "fmt"
  "os"
  "path/filepath"
)

func main() {
  ex, err := os.Executable()
  if err != nil {
    panic(err)
  }
  // Path to executable file
  fmt.Println(ex)
  // Resolve the direcotry of the executable
  exPath := filepath.Dir(ex)
  fmt.Println("Executable path :" + exPath)
  // Use EvalSymlinks to get the real path.
  realPath, err := filepath.EvalSymlinks(exPath)
  if err != nil {
    panic(err)
  }
  fmt.Println("Symlink evaluated:" + realPath)
}
```

The following recipe for the current PID seems not working correctly in Windows / Cygwin:

```go
package main

import (
  "fmt"
  "os"
  "os/exec"
)

func main() {
  pid := os.Getpid()
  fmt.Printf("Process PID: %d \n", pid)
  prc := exec.Command("ps")
  out, err := prc.Output()
  if err != nil {
    panic(err)
  }
  fmt.Println(string(out))
}
```

