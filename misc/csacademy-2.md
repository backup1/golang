# CsAcademy 2

```go
package main

import "fmt"

type pt struct {
    x,y int
}

func main() {
    var t,i,j,k,x,y int
    fmt.Scanln(&t)
    for i = 0; i < t; i++ {
        var v []pt
        for j = 0; j < 4; j++ {
            fmt.Scanln(&x,&y)
            v = append(v,pt{x,y})
        }
        var m map[int]int = make(map[int]int)
        for j = 0; j < 4; j++ {
            for k = j+1; k < 4; k++ {
                var dx int = v[k].x-v[j].x
                var dy int = v[k].y-v[j].y
                var d int = dx*dx+dy*dy
                m[d]++
            }
        }
        if len(m) != 2 {
            fmt.Println(0)
        } else {
            var ok bool = true
            var d1,d2 int
            for j,k = range m {
                if k == 4 {
                    d1 = j
                } else if k == 2 {
                    d2 = j
                } else {
                    ok = false
                }
            }
            if ok == true && d2 == 2*d1 {
                fmt.Println(1)
            } else {
                fmt.Println(0)
            }
        }
    }
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

type cpl struct{
    b,e int
}

func main() {
    var n,i,b,e int
    fmt.Scanln(&n)
    var m map[cpl]bool = make(map[cpl]bool)
    scanner := bufio.NewScanner(os.Stdin)
	scanner.Split(bufio.ScanWords)
    for i = 1; i < n; i++ {
        scanner.Scan()
		b, _ = strconv.Atoi(scanner.Text())
        scanner.Scan()
		e, _ = strconv.Atoi(scanner.Text())
        if b < e {
            b,e = e,b
        }
        m[cpl{b,e}] = true
    }
    var cnt int = 0;
    for i = 1; i < n; i++ {
        scanner.Scan()
		b, _ = strconv.Atoi(scanner.Text())
        scanner.Scan()
		e, _ = strconv.Atoi(scanner.Text())
        if b < e {
            b,e = e,b
        }
        if _,ok := m[cpl{b,e}]; ok {
            cnt++
        }
    }
    fmt.Print(cnt)
}
```

```go
package main

import "fmt"

func main() {
    var n,i,j,x int
    fmt.Scanln(&n)
    var m [][]int
    for i = 0; i < n; i++ {
        var v []int
        for j = 0; j < n; j++ {
            fmt.Scan(&x)
            v = append(v,x)
        }
        m = append(m,v)
    }
    for i = 0; i < n; i++ {
        for j = 0; j < n; j++ {
            if m[i][j] == 1 || m[j][n-i-1] == 1 || m[n-j-1][i] == 1 || m[n-i-1][n-j-1] == 1 {
                fmt.Print("1 ")
            } else {
                fmt.Print("0 ")
            }
        }
        fmt.Println()
    }
}
```

```go
package main

import "fmt"

func main() {
    var n,m,i,x,tot int
    fmt.Scanln(&n,&m)
    tot = 0
    for i = 0; i < m; i++ {
        fmt.Scan(&x)
        tot += x
        if 2*tot == n {
            fmt.Print(-1)
            break
        }
        if 2*tot > n {
            fmt.Print(i+1)
            break
        }
    }
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
    var n,e1,e2,i,ans,a,b int
    fmt.Scanln(&n,&e1,&e2)
    if e1 > e2 {
        e1,e2 = e2,e1
    }
    ans = 0
    scanner := bufio.NewScanner(os.Stdin)
	scanner.Split(bufio.ScanWords)
    for i = 0; i < n; i++ {
        scanner.Scan()
		a,_ = strconv.Atoi(scanner.Text())
        scanner.Scan()
		b,_ = strconv.Atoi(scanner.Text())
        if a >= b && a <= e2 {
            ans++
        } else if a < b && a >= e1 {
            ans++
        }
    }
    fmt.Print(ans)
}
```

```go
package main

import "fmt"

func main() {
    var n,i,a,winner int
    fmt.Scanln(&n)
    var v,cnt []int
    for i = 0; i < n; i++ {
        fmt.Scan(&a)
        v = append(v,a)
        cnt = append(cnt,0)
    }
    winner = 0
    for i = 1; i < n; i++ {
        if v[winner] < v[i] {
            winner = i
        }
        cnt[winner]++
    }
    for i = 0; i < n; i++ {
        fmt.Printf("%d ",cnt[i])
    }
}
```

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
	"sort"
)

func main() {
    var h,w,n,m int
    fmt.Scanln(&h,&w,&n,&m)
    scanner := bufio.NewScanner(os.Stdin)
	scanner.Split(bufio.ScanWords)
	var x,y,z map[int]int
	var i,a int
	y = make(map[int]int)
	z = make(map[int]int)
	var ys [] int
	for i = 0; i < n; i++ {
	    scanner.Scan()
	    a, _ = strconv.Atoi(scanner.Text())
	    ys = append(ys,a)
	}
	sort.Ints(ys)
    var prev int = 0
    var crt int
	for _,crt = range ys {
	    y[crt-prev]++
	    z[crt-prev] = 1
	    prev = crt
	}
	y[h-prev]++
	z[h-prev] = 1
	prev = 0
	x = make(map[int]int)
	var xs [] int
	for i = 0; i < m; i++ {
	    scanner.Scan()
	    a, _ = strconv.Atoi(scanner.Text())
	    xs = append(xs,a)
	}
	sort.Ints(xs)
	for _,crt = range xs {
	    x[crt-prev]++
	    z[crt-prev] = 1
	    prev = crt
	}
	x[w-prev]++
	z[w-prev] = 1
    var ans int = 0
    for key,_ := range z {
        ans += x[key]*y[key]
    }
    fmt.Print(ans)
}
```

```go
package main

import "fmt"

func main() {
    var n,i int
    fmt.Scanln(&n)
    var m map[byte]int = make(map[byte]int)
    var c string
    for i = 0; i < n; i++ {
        fmt.Scan(&c)
        var bc byte = (byte)(c[0]) 
        m[bc]++
    }
    var s string
    fmt.Scan(&s)
    var bs = ([]byte)(s)
    var ans int = 0
    var d byte
    for _,d = range bs {
        if m[d] > 0 {
            m[d]--
        } else {
            ans++
        }
    }
    fmt.Print(ans)
}
```

```go
package main

import "fmt"

func main() {
    var n,i int
    fmt.Scanln(&n)
    var s string
    fmt.Scanln(&s)
    var b int = 0
    var ans int = 0
    var cnt int = 0
    for i = 0; i < n; i++ {
        if s[i] == '1' {
            cnt++
        }
        if cnt == 3 {
            if ans < i-b {
                ans = i-b
            }
            for s[b] == '0' {
                b++
            }
            b++
            cnt = 2
        }
    }
    if ans < n-b {
        ans = n-b
    }
    fmt.Print(ans+1)
}
```

```go
package main

import "fmt"

func main() {
    var n int
    fmt.Scanln(&n)
    n--
    n %= 10
    if n == 0 || n == 3 || n == 6 {
        fmt.Print(1)
    } else if n == 9 {
        fmt.Print(4)
    } else if n == 1 || n == 4 || n == 7 {
        fmt.Print(2)
    } else {
        fmt.Print(3)
    }
}
```

```go
package main

import "fmt"

func main() {
    var n,k,i int
    fmt.Scanln(&n,&k)
    var s string
    fmt.Scanln(&s)
    var has1 bool = false
    for i = 0; i < len(s); i++ {
        if s[i] == '1' {
            has1 = true
            break
        }
    }
    if has1 == false {
        fmt.Print(n*k)
    } else {
        if k > 1 {
            s += s
        }
        var cnt int = 0
        var ans int = 0
        for i = 0; i < len(s); i++ {
            if s[i] == '0' {
                cnt++
            } else {
                if ans < cnt {
                    ans = cnt
                }
                cnt = 0
            }
        }
        if ans < cnt {
            ans = cnt
        }
        fmt.Print(ans)
    }
}
```

```go
package main

import "fmt"

func main() {
    var a,b,i int
    fmt.Scan(&a)
    fmt.Scan(&a)
    fmt.Scan(&a)
    fmt.Scan(&a)
    for i = 4; i < 16; i++ {
        fmt.Scan(&b)
        if b+300 <= a {
            fmt.Print(i)
            return
        }
    }
    fmt.Print(16)
}
```

