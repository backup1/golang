# Fast Input / Output

```go
package main

import (
  "bufio"
  "fmt"
)

var reader *bufio.Reader = bufio.NewReader(os.Stdin)
var writer *bufio.Writer = bufio.NewWriter(os.Stdout)
func printf(f string, a ...interface{}) { fmt.Fprintf(writer, f, a...) }
func scanf(f string, a ...interface{}) { fmt.Fscanf(reader, f, a...) }

func main() {
  // STDOUT MUST BE FLUSHED MANUALLY!!!
  defer writer.Flush()

  var a, b int
  scanf("%d %d\n", &a, &b)
  printf("%d\n", a+b)
}
```

```go
package main

import (
    "fmt"
    "os"
    "bufio"
    "strings"
    "strconv"
)

type Scanner struct {

    reader *bufio.Reader
    buffer []string
    pointer int
}

func NewScanner() *Scanner {
    return &Scanner{
        reader: bufio.NewReaderSize(os.Stdin,4096),
        pointer: 0,
    }
}

func (self *Scanner) NextLine () string {
    var buffer []byte
    for {
        line,isPrefix,_ := self.reader.ReadLine()
        buffer = append(buffer, line...)
        if !isPrefix {
            break
        }
    }
    return string(buffer)
}

func (self *Scanner) Next () string {
    if self.pointer >= len(self.buffer) {
        line := self.NextLine()
        self.buffer = strings.Fields(line)
        self.pointer = 0
    }
    self.pointer++
    return self.buffer[self.pointer-1]
}

func (self *Scanner) NextInt () int {
    s := self.Next()
    i,_ := strconv.ParseInt(s,10,32)
    return int(i)
}

func (self *Scanner) NextLong () int64{
    s := self.Next()
    l,_ := strconv.ParseInt(s,10,64)
    return int64(l)
}

func (self *Scanner) NextFloat () float32 {
    s := self.Next()
    f,_ := strconv.ParseFloat(s,32)
    return float32(f)
}

func (self *Scanner) NextDouble () float64 {
    s := self.Next()
    d,_ := strconv.ParseFloat(s,64)
    return float64(d)
}

func main () {
    cin := NewScanner()

    N := cin.NextInt()
    K := cin.NextLong()

    H := make([]int64,N)
    for i := 0;i < N;i++ {
        H[i] = cin.NextLong()
    }

    low := int64(0)
    high := int64(1000000000+1)
    for high - low > 1 {
        mid := int64((high + low) / 2)
        count := int64(0)
        for i := 0;i < N;i++ {
            count += int64(H[i] / mid)
        }

        if count >= K {
            low = mid
        } else {
            high = mid
        }
    }
    fmt.Println(low)
}
```

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
)

func main() {
	var n, k int
	fmt.Scanf("%d %d\n", &n, &k)
	var h_sum int
	heights := make([]int, n)
	max := 0

	scanner := bufio.NewScanner(os.Stdin)
	scanner.Split(bufio.ScanWords)

	for i := 0; i < n; i++ {
		scanner.Scan()
		heights[i], _ = strconv.Atoi(scanner.Text())
		h_sum += heights[i]
		if (heights[i] > max) {
			max = heights[i]
		}
	}
	l := 0
	h := max + 1
	for h - l > 1 {
		mid := (l + h) / 2
		t := 0
		for i := 0; i < n; i++ {
			t += heights[i] / mid
		}
		if t < k {
			h = mid
		} else {
			l = mid
		}
	}
	fmt.Println(l)
}
```

