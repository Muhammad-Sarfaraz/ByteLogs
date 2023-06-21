# Hands on Note for Go Lang

#### String:

```
str := "Hello"

```

### Packages
```
import "fmt"
import "math/rand"
import (
  "fmt"        // gives fmt.Println
  "math/rand"  // gives rand.Intn
)
```

#### Wait Group
```
import "sync"

func main() {
  var wg sync.WaitGroup
  
  for _, item := range itemList {
    // Increment WaitGroup Counter
    wg.Add(1)
    go doOperation(&wg, item)
  }
  // Wait for goroutines to finish
  wg.Wait()
  
}
```
