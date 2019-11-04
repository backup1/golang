# CsAcademy

```go
package main

import "fmt"

func min(x,y int64) int64 {
    if x < y {
        return x
    } else {
        return y
    }
}

func main() {
    var n,m,x,y int64
    fmt.Scanln(&n,&m,&x,&y)
    fmt.Print(min(n,(m+n*y)/(x+y)))
}
```

```go
package main

import (
    "fmt"
    "sort"
)

type Node struct {
    s string
    idx int
}

func main() {
    var n,idx,i int
    var s string
    fmt.Scanln(&n)
    var list []Node
    for i = 0; i < n; i++ {
        fmt.Scanln(&s,&idx)
        var ns Node
        ns.s = s
        ns.idx = i+1
        list = append(list,ns)
    }
    sort.Slice(list,func(i,j int) bool {
        return list[i].s < list[j].s
    })
    for i = 0; i < n; i++ {
        fmt.Printf("%d ",list[i].idx)
    }
}
```

```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    var n,i int
    fmt.Scanln(&n)
    var s string
    var c byte
    var list []byte
    for i = 0; i < n; i++ {
        fmt.Scanln(&s)
        var bs = ([]byte)(s)
        var z byte = 'z'
        for _,c = range bs {
            if c < z {
                z = c
            }
        }
        list = append(list,z)
    }
    sort.Slice(list,func(i,j int) bool {
        return list[i] < list[j]
    })
    for _,c = range list {
        fmt.Printf("%c",c)
    }
}
```

```go
package main

import "fmt"

func main() {
    var i,j,x int
    var a,b []int
    for i = 0; i < 6; i++ {
        fmt.Scan(&x)
        a = append(a,x)
    }
    for i = 0; i < 6; i++ {
        fmt.Scan(&x)
        b = append(b,x)
    }
    var cnt = make(map[int]int)
    for i = 0; i < 6; i++ {
        for j = 0; j < 6; j++ {
            cnt[a[i]+b[j]]++
        }
    }
    var ans,maxcnt int
    maxcnt = -1
    for i,x = range cnt {
        if x > maxcnt {
            maxcnt = x
            ans = i
        } else if x == maxcnt {
            if i < ans {
                ans = i
            }
        }
    }
    fmt.Print(ans)
}
```

```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    var n,i,a,tot int
    fmt.Scanln(&n)
    var v []int
    for i = 0; i < n; i++ {
        fmt.Scan(&a)
        v = append(v,a)
    }
    sort.Slice(v,func(i,j int) bool {
        return v[i] < v[j]
    })
    tot = 0
    for i = 1; i < n-1; i++ {
        tot += v[i]
    }
    fmt.Print(tot/(n-2))
}
```

```go
package main

import (
    "fmt"
    "sort"
)

type food struct {
    total int
    poison int
    idx int
}

func main() {
    var n,i,t,p int
    fmt.Scanln(&n)
    var v []food
    for i = 0; i < n; i++ {
        fmt.Scanln(&t,&p)
        v = append(v,food{t,p,i+1})
    }
    sort.Slice(v,func(i,j int) bool {
        return v[i].poison*v[j].total < v[i].total*v[j].poison
    })
    fmt.Print(v[0].idx)
}
```

```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    var n,m,i,x int
    fmt.Scanln(&n,&m)
    var a,b []int
    for i = 0; i < n; i++ {
        fmt.Scan(&x)
        a = append(a,x)
    }
    for i = 0; i < m; i++ {
        fmt.Scan(&x)
        b = append(b,x)
    }
    sort.Ints(a)
    sort.Ints(b)
    var ans1,ans2,idx int
    ans1 = 0
    ans2 = 0
    idx = m-1
    for i = n-1; i >= 0; i-- {
        if idx < 0 {
            break
        }
        if a[i] <= b[idx] {
            ans2++
        } else {
            ans1++
        }
        idx--
    }
    fmt.Printf("%d %d",ans1,ans2)
}
```

```go
package main

import "fmt"

type seg struct {
    b,e int
}

func main() {
    var n,i,b,e int
    fmt.Scanln(&n)
    var v []seg
    for i = 0; i < n; i++ {
        fmt.Scanln(&b,&e)
        v = append(v,seg{b,e})
    }
    var ans int = 0
    var p,p1 seg
    for _,p = range v {
        for _,p1 = range v {
            if p1.b < p.b && p.e < p1.e {
                ans++
                break
            }
        }
    }
    fmt.Print(ans)
}
```

```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    var s,q,k,p,i float64
    fmt.Scanln(&s,&q,&k)
    var v []float64
    for i = 0; i < q; i++ {
        fmt.Scan(&p)
        v = append(v,p)
    }
    sort.Float64s(v)
    var ans float64 = s
    for _,p = range v {
        if ans + k > ans + ans*p*0.01 {
            ans += k
        } else {
            ans *= 1.0 + p*0.01
        }
    }
    fmt.Print(ans)
}
```

```go
package main

import "fmt"

func main() {
    var r1,c1,r2,c2 int
    fmt.Scanln(&r1,&c1,&r2,&c2)
    if r1 == r2 && c1 == c2 {
        fmt.Print(0)
    } else if (r1+c1+r2+c2)%2 == 1 {
        fmt.Print(-1)
    } else if r1+c1 == r2+c2 || r1-c1 == r2-c2 {
        fmt.Print(1)
    } else {
        fmt.Print(2)
    }
}
```

```go
package main

import "fmt"

func main() {
    var a,b,i int
    fmt.Scanln(&a,&b)
    var nb int = -1
    var ans int = a
    for i = a; i <= b; i++ {
        var cnt int = 0
        var crt int = i
        for {
            var crtd = crt%10
            if crtd == 8 {
                cnt += 2
            } else if crtd == 0 || crtd == 6 || crtd == 9 {
                cnt++
            }
            if crt < 10 {
                break
            }
            crt /= 10
        }
        //fmt.Println(i,cnt)
        if cnt > nb {
            nb = cnt
            ans = i
        }
    }
    fmt.Print(ans)
}
```

```go
package main

import (
    "fmt"
    "bufio"
    "os"
    "strconv"
)

func main() {
    var n,k,i,x,tot,highest int64
    fmt.Scanln(&n,&k)
    tot = 0
    highest = 0
    var v []int64
    scanner := bufio.NewScanner(os.Stdin)
    scanner.Split(bufio.ScanWords)
    for i = 0; i < n; i++ {
        scanner.Scan()
        x,_ = strconv.ParseInt(scanner.Text(),10,64)
        v = append(v,x)
        tot += x
        if highest < x {
            highest = x
        }
    }
    var ans int64 = 0
    var low int64 = 1
    var high int64 = 1000000000
    if high > highest {
        high = highest
    }
    if high > tot/k {
        high = tot/k
    }
    for low <= high {
        var mid int64 = (low+high)/2
        var nb int64 = 0
        for _,x = range v {
            nb += x/mid
        }
        if nb >= k {
            if ans < mid {
                ans = mid
            }
            low = mid+1
        } else {
            high = mid-1
        }
    }
    fmt.Print(ans)
}
```

```go
package main

import "fmt"

func main() {
    var n,w,a,b,i,tot,idx int
    fmt.Scanln(&n,&w)
    tot = 0
    idx = 0
    var done bool = false
    for i = 1; i <= n; i++ {
        fmt.Scanln(&a,&b)
        if a == 1 {
            tot += b
            if idx == 0 {
                idx = i
            }
            if tot >= w {
                fmt.Print(idx)
                return
            }
        } else {
            idx = 0
            tot = 0
        }
    }
    if !done {
        fmt.Print(-1)
    }
}
```

```go
package main

import "fmt"

func main() {
    var n,i,a,cnt1,cnt2 int
    fmt.Scanln(&n)
    cnt1 = 0
    cnt2 = 0
    for i = 0; i < 2*n; i++ {
        fmt.Scan(&a)
        if a == 0 {
            if i%2 == 1 {
                cnt1++
            } else {
                cnt2++
            }
        }
    }
    var cnt int = cnt1
    if cnt2 < cnt {
        cnt = cnt2
    }
    fmt.Print(cnt)
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
    var n,i,x int
    fmt.Scanln(&n)
    var left,right []int
	scanner := bufio.NewScanner(os.Stdin)
	scanner.Split(bufio.ScanWords)
	for i = 0; i < n; i++ {
	    scanner.Scan()
		x, _ = strconv.Atoi(scanner.Text())
		left = append(left,x)
	}
	for i = 0; i < n; i++ {
	    scanner.Scan()
		x, _ = strconv.Atoi(scanner.Text())
		right = append(right,x)
	}
    for i = 0; i < n; i++ {
        if i < n-1 && left[i] < left[i+1] {
            fmt.Print(0)
        } else if i > 0 && right[i] < right[i-1] {
            fmt.Print(0)
        } else {
            fmt.Print(1)
        }
    }
}
```

```go
package main

import "fmt"

func main() {
    var s,a,b string
    fmt.Scanln(&s)
    fmt.Scanln(&a)
    fmt.Scanln(&b)
    var ls int = len(s)
    var la int = len(a)
    var idx int = 0
    var i int
    for idx < ls {
        if idx+la <= ls {
            var ok bool = true
            for i = 0; i < la; i++ {
                if a[i] != s[idx+i] {
                    ok = false
                    break
                }
            }
            if ok {
                fmt.Print(b)
                idx += la
            } else {
                ok = true
                for i = 0; i < la; i++ {
                    if b[i] != s[idx+i] {
                        ok = false
                        break
                    }
                }
                if ok {
                    fmt.Print(a)
                    idx += la
                } else {
                    fmt.Printf("%c",s[idx])
                    idx++
                }
            }
        } else {
            fmt.Printf("%c",s[idx])
            idx++
        }
    } 
}
```

```go
package main

import "fmt"

func main() {
    var x1,x2,x3 int
    fmt.Scanln(&x1,&x2,&x3)
    var d12 = x1 - x2
    if d12 < 0 {
        d12 = -d12
    }
    var d23 = x2 - x3
    if d23 < 0 {
        d23 = -d23
    }
    var d13 = x1 - x3
    if d13 < 0 {
        d13 = -d13
    }
    if d13 < d23 {
        fmt.Print(d12+d13)
    } else {
        fmt.Print(d12+d23)
    }
}
```

```text
package main

import "fmt"

func main() {
    var n,i,a,tot int
    fmt.Scanln(&n)
    tot = 0
    for i = 0; i < n; i++ {
        fmt.Scan(&a)
        tot += a
    }
    fmt.Print(tot&1)
}
```

```go
package main

import "fmt"

func main() {
    m := map[string]int{
        "Monday" : 1,
        "Tuesday" : 2,
        "Wednesday" : 3,
        "Thursday" : 4,
        "Friday" : 5,
        "Saturday" : 6,
        "Sunday" : 7,
    }
    v := []int{31,28,31,30,31,30,31,31,30,31,30}
    var s string
    fmt.Scanln(&s)
    var nb int = m[s]+12
    var cnt int = 0
    if nb%7 == 5 {
        cnt++
    }
    var i int
    for _,i = range v {
        nb += i
        if nb%7 == 5 {
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
    var n,i,j,k int
    fmt.Scanln(&n)
    var s string
    var ss []string
    for i = 0; i < n; i++ {
        fmt.Scanln(&s);
        ss = append(ss,s)
    }
    for i = 0; i < n; i++ {
        var ok bool = false
        for j = 0; j < n; j++ {
            if j == i {
                continue
            }
            for k = 0; k < n; k++ {
                if k == i || k == j {
                    continue;
                }
                if ss[i] == ss[j]+ss[k] {
                    ok = true
                    break
                }
            }
            if ok == true {
                break
            }
        }
        if ok == true {
            fmt.Printf("%d ",i+1)
        }
    }
}
```

```go
package main

import "fmt"

func main() {
    var n,i,j,ans int
    fmt.Scanln(&n)
    var v []int
    for i = 0; i < n; i++ {
        fmt.Scan(&j)
        v = append(v,j)
    }
    ans = 0
    for i = 0; i < n; i++ {
        var cnt int = 0
        for j = 0; j < n; j++ {
            if (v[j]-i-j)%n == 0 {
                cnt++
            }
        }
        if ans < cnt {
            ans = cnt
        }
    }
    fmt.Print(ans)
}
```

