# Dictionary

```go
package main

import (
  "fmt"
  "sync"
)

type DictKey string
type DictVal string

type Dictionary struct {
  elements map[DictKey]DictVal
  lock sync.RWMutex
}

func (dict *Dictionary) Put(key DictKey,value DictVal) {
  dict.lock.Lock()
  defer dict.lock.Unlock()
  if dict.elements == nil {
    dict.elements = make(map[DictKey]DictVal)
  }
  dict.elements[key] = value
}

func (dict *Dictionary) Remove(key DictKey) bool {
  dict.lock.Lock()
  defer dict.lock.Unlock()
  var exists bool
  _,exists = dict.elements[key]
  if exists {
    delete(dict.elements,key)
  }
  return exists
}

func (dict *Dictionary) Contains(key DictKey) bool {
  dict.lock.RLock()
  defer dict.lock.RUnlock()
  var exists bool
  _,exists = dict.elements[key]
  return exists
}

func (dict *Dictionary) Find(key DictKey) DictVal {
  dict.lock.RLock()
  defer dict.lock.RUnlock()
  return dict.elements[key]
}

func (dict *Dictionary) Reset() {
  dict.lock.Lock()
  defer dict.lock.Unlock()
  dict.elements = make(map[DictKey]DictVal)
}

func (dict *Dictionary) NumberOfElements() int {
  dict.lock.RLock()
  defer dict.lock.RUnlock()
  return len(dict.elements)
}

func (dict *Dictionary) GetKeys() []DictKey {
  dict.lock.RLock()
  defer dict.lock.RUnlock()
  var dictKeys []DictKey = []DictKey{}
  var key DictKey
  for key = range dict.elements {
    dictKeys = append(dictKeys,key)
  }
  return dictKeys
}

func (dict *Dictionary) GetValues() []DictVal {
  dict.lock.RLock()
  defer dict.lock.RUnlock()
  var dictValues []DictVal = []DictVal{}
  var key DictKey
  for key = range dict.elements {
    dictValues = append(dictValues,dict.elements[key])
  }
  return dictValues
}

func main() {
  var dict *Dictionary = &Dictionary{}
  dict.Put("1","1")
  dict.Put("2","2")
  dict.Put("3","3")
  dict.Put("4","4")
  fmt.Println(dict)
}
```

