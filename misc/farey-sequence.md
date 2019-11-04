# Farey Sequence

```go
package main

import "fmt"

type fraction struct {
  numerator int
  denominator int
}

func (frac fraction) String() string {
  return fmt.Sprintf("%d/%d",frac.numerator,frac.denominator)
}

func g(l fraction, r fraction, num int) {
  var frac fraction = fraction{l.numerator+r.numerator, l.denominator+r.denominator}
  if frac.denominator <= num {
    g(l,frac,num)
    fmt.Print(frac, " ")
    g(frac,r,num)
  }
}

func main() {
  var num int
  var l,r fraction
  for num = 1; num <= 11; num++ {
    l = fraction{0,1}
    r = fraction{1,1}
    fmt.Printf("F(%d): %s ",num,l)
    g(l,r,num)
    fmt.Println(r)
  }
}
```

