# Hash

```go
package main

import (
  "bytes"
  "crypto/sha256"
  "encoding"
  "fmt"
  "log"
  "hash"
)

func main() {
  const (
    example1 = "this is a example "
    example2 = "second example"
  )
  var firstHash hash.Hash
  firstHash = sha256.New()
  firstHash.Write([]byte(example1))
  var marshaler encoding.BinaryMarshaler
  var ok bool
  marshaler,ok = firstHash.(encoding.BinaryMarshaler)
  if !ok {
    log.Fatal("first Hash is not generated by encoding.BinaryMarshaler")
  }
  var data []byte
  var err error
  data,err = marshaler.MarshalBinary()
  if err != nil {
    log.Fatal("failure to create first Hash:",err)
  }
  var secondHash hash.Hash
  secondHash = sha256.New()
  var unmarshaler encoding.BinaryUnmarshaler
  unmarshaler,ok = secondHash.(encoding.BinaryUnmarshaler)
  if !ok {
    log.Fatal("second Hash is not generated by encoding.BinaryUnmarshaler")
  }
  if err := unmarshaler.UnmarshalBinary(data); err != nil {
    log.Fatal("failure to create hash:",err)
  }
  firstHash.Write([]byte(example2))
  secondHash.Write([]byte(example2))
  fmt.Printf("%x\n", firstHash.Sum(nil))
  fmt.Println(bytes.Equal(firstHash.Sum(nil),secondHash.Sum(nil)))
}
```

```go
package main

import (
  "fmt"
  "crypto/sha1"
  "hash"
)

func CreateHash(byteStr []byte) []byte {
  var hashVal hash.Hash = sha1.New()
  hashVal.Write(byteStr)
  var bytes []byte = hashVal.Sum(nil)
  return bytes
}

func CreateHashMultiple(byteStr1 []byte, byteStr2 []byte) []byte {
  return xor(CreateHash(byteStr1), CreateHash(byteStr2))
}

func xor(byteStr1 []byte, byteStr2 []byte) []byte {
  var xorbytes []byte = make([]byte,len(byteStr1))
  var i int
  for i = 0; i < len(byteStr1); i++ {
    xorbytes[i] = byteStr1[i]^byteStr2[i]
  }
  return xorbytes
}

func main() {
  var bytes []byte = CreateHashMultiple([]byte("Check"), []byte("Hash"))
  fmt.Printf("%x\n", bytes)
}
```
