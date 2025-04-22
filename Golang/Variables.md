# Variables

In Go, variables are explicitly declared and used by the compiler to e.g. check type-correctness of function calls.

var declares 1 or more variables.

You can declare multiple variables at once.

Go will infer the type of initialized variables.

Variables declared without a corresponding initialization are zero-valued. For example, the zero value for an int is 0.

The := syntax is shorthand for declaring and initializing a variable, e.g. for var f string = "apple" in this case. This syntax is only available inside functions.

```go
package main

import "fmt"

func main() {

    var a = "initial"
    fmt.Println(a)

    var b, c int = 1, 2
    fmt.Println(b, c)

    var d = true
    fmt.Println(d)

    var e int
    fmt.Println(e)

    f := "apple"
    fmt.Println(f)
}
```

## Difference Between var and :=

- var
  - Can be used inside and outside of functions
  - Variable declaration and value assignment can be done separately

- :=
  - Can only be used inside functions
  - Variable declaration and value assignment cannot be done separately (must be done in the same line)
