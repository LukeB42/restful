## Restful

#### A Gorilla-based fork of Sleepy for Go

Restful is a drop-in library for RESTful APIs.

```go
package main

import (
    "net/url"
    "net/http"
    "github.com/LukeB42/restful"
)

// Create something to bind our HTTP verb-methods to
type Item struct { }

func (item Item) Get(values url.Values, headers http.Header) (int, interface{}, http.Header) {
    items := []string{"item1", "item2"}
    data := map[string][]string{"items": items}
    return 200, data, http.Header{"Content-type": {"application/json"}}
}

func main() {
    item := new(Item)

    api := sleepy.NewAPI()
    api.AddResource(item, "/items")
    api.Start(3000)
}
```

Now if we curl that endpoint:

```bash
$ curl localhost:3000/items
{"items": ["item1", "item2"]}
```


## Credits

Cheers to Doug Black for the original Sleepy code.

## License

`restful` is released under the [MIT License](http://opensource.org/licenses/MIT).
