# Thue-Morse sequence

```go
package main

import (
  "bytes"
  "fmt"
)

func ThueMorseSequence(buffer *bytes.Buffer) {
  var b,crtLength int
  var crtBytes []byte
  for b,crtLength,crtBytes = 0,buffer.Len(),buffer.Bytes(); b < crtLength; b++ {
    if crtBytes[b] == '1' {
      buffer.WriteByte('0')
    } else {
      buffer.WriteByte('1')
    }
  }
}

func main() {
  var buffer bytes.Buffer
  // initial sequence member is "0"
  buffer.WriteByte('0')
  fmt.Println(buffer.String())
  var i int
  for i = 2; i <= 7; i++ {
    ThueMorseSequence(&buffer)
    fmt.Println(buffer.String())
  }
}
```

