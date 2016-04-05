## Restful

Gorilla-based drop-in library for RESTful APIs.

```bash
go get github.com/LukeB42/restful
go get github.com/gorilla/mux
go get github.com/gorilla/handlers
```


```go
package main

import (
    "fmt"
    "github.com/gorilla/mux"
    "github.com/LukeB42/restful"
    "net/http"
    "os"
)

// Create something to bind our HTTP verb-methods to
type Item struct { }

func (item Item) Get(rw *http.ResponseWriter, request *http.Request) (int, interface{}, http.Header) {
	vars := mux.Vars(request)
	if name, ok := vars["name"]; ok {
		greeting := fmt.Sprintf("Hello, %v!\n", name)
		return 200, greeting, http.Header{"Content-Type": {"text/html"}}
	}
	items := []string{"item1", "item2"}
	data := map[string][]string{"items": items}
	return 200, data, http.Header{"Content-type": {"application/json"}}
}

func main() {
    item := new(Item)

    api := restful.NewAPI()
    api.AddResource(item, "/items")
    api.AddResource(item, "/items/{name}")
    api.Start(":3000", os.Stdout)
}
```

Now if we curl that endpoint:

```bash
$ curl localhost:3000/items
{"items": ["item1", "item2"]}
```


## Credits

Based on [Sleepy](https://github.com/dougblack/sleepy) by Doug Black.

## License

`restful` is released under the [MIT License](http://opensource.org/licenses/MIT).
