# Advanced JSON library

The project is a standard `encoding/json` package from the [Golang sources](https://github.com/golang/go), with a small  feature.
I added the **MarshalTag()** function that allows to specify a structure tag when marshaling (by default tag is `json`).

#### Example
```golang
type St struct {
	Id    string   `json:"id" web:"id"`
	Count int      `json:"count" web:"len"`
	Items []string `json:"items" web:"-"`
}

var t = St{
	Id:    "testId",
	Count: 99,
	Items: []string{"A", "B", "C"},
}

func main() {

	b, _ := json.MarshalTag(t, "json")
	fmt.Println(string(b))
	// {"id":"testId","count":99,"items":["A","B","C"]}

	b, _ = json.MarshalTag(t, "web")
	fmt.Println(string(b))
	// {"id":"testId","len":99}

}
```
