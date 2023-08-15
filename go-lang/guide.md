# Hands on Note for Go-Lang











Go has three basic data types:

bool: represents a boolean value and is either true or false
Numeric: represents integer types, floating point values, and complex types
string: represents a string value


# Setup

#### Make A API [ Demo Example ]
```
import (
   "io/ioutil"
   "log"
   "net/http"
)

func main() {
   resp, err := http.Get("https://jsonplaceholder.typicode.com/posts")
   if err != nil {
      log.Fatalln(err)
   }
//We Read the response body on the line below.
   body, err := ioutil.ReadAll(resp.Body)
   if err != nil {
      log.Fatalln(err)
   }
//Convert the body to type string
   sb := string(body)
   log.Printf(sb)
}
```

#### Concurrent:

#### String:

```
str := "Hello"

```

### Packages:
```
import "fmt"
import "math/rand"
import (
  "fmt"        // gives fmt.Println
  "math/rand"  // gives rand.Intn
)
```

#### Wait Group:
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
