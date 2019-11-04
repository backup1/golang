# Channel with timeout interval

```go
package main

import (
  "errors"
  "log"
  "time"
)

func delayTimeOut(channel chan interface{}, timeOut time.Duration) (interface{}, error) {
  log.Printf("delayTimeOut enter")
  defer log.Printf("delayTimeOut exit")
  var data interface{}
  select {
  case <-time.After(timeOut):
    return nil, errors.New("delayTimeOut time out")
  case data = <-channel:
    return data, nil
  }
}

func main() {
  channel := make(chan interface{})
  go func() {
    var err error
    var data interface{}
    data, err = delayTimeOut(channel, time.Second)
    if err != nil {
      log.Printf("error %v", err)
      return
    }
    log.Printf("data %v", data)
  }()
  channel <- struct{}{}
  time.Sleep(time.Second * 2)
  go func() {
    var err error
    var data interface{}
    data, err = delayTimeOut(channel, time.Second)
    if err != nil {
      log.Printf("error %v", err)
      return
    }
    log.Printf("data %v", data)
  }()
  time.Sleep(time.Second * 2)
}
```

Using context instead of channel

```go
package main

import (
  "errors"
  "golang.org/x/net/context"
  "log"
  "time"
)

func main() {
  var delay time.Duration = time.Millisecond
  var cancel context.CancelFunc
  var contex context.Context
  contex, cancel = context.WithTimeout(context.Background(), delay)
  go func(context.Context) {
    <-contex.Done()
    log.Printf("contex done")
  }(contex)
  _ = cancel
  time.Sleep(delay * 2)
  log.Printf("contex end %v", contex.Err())
  channel := make(chan struct{})
  var err error
  go func(chan struct{}) {
    select {
    case <-time.After(delay):
      err = errors.New("ch delay")
    case <-channel:
    }
    log.Printf("channel done")
  }(channel)
  time.Sleep(delay * 2)
  log.Printf("channel end %v", err)
}
```

