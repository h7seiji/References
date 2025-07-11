# Maps

A map maps keys to values.

The zero value of a map is nil. A nil map has no keys, nor can keys be added.

The make function returns a map of the given type, initialized and ready for use.

```go
package main

import "fmt"

type Vertex struct {
 Lat, Long float64
}

var m map[string]Vertex

func main() {
 m = make(map[string]Vertex)
 m["Bell Labs"] = Vertex{
  40.68433, -74.39967,
 }
 fmt.Println(m["Bell Labs"])
}
```

## Map literals

Map literals are like struct literals, but the keys are required.

If the top-level type is just a type name, you can omit it from the elements of the literal.

```go
package main

import "fmt"

type Vertex struct {
 Lat, Long float64
}

var m = map[string]Vertex{
 "Bell Labs": Vertex{
  40.68433, -74.39967,
 },
 "Google": Vertex{
  37.42202, -122.08408,
 },
}

func main() {
 fmt.Println(m)
}
```

## Mutating Maps

Insert or update an element in map m:

```go
m[key] = elem
```

Retrieve an element:

```go
elem = m[key]
```

Delete an element:

```go
delete(m, key)
```

Test that a key is present with a two-value assignment:

```go
elem, ok = m[key]
```

If key is in m, ok is true. If not, ok is false.

If key is not in the map, then elem is the zero value for the map's element type.

Note: If elem or ok have not yet been declared you could use a short declaration form:

```go
elem, ok := m[key]
```
