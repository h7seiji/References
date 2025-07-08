# Functions

A function can take zero or more arguments.

In this example, add takes two parameters of type int.

Notice that the type comes after the variable name.

When two or more consecutive named function parameters share a type, you can omit the type from all but the last.

```go
package main

import "fmt"

func add(x int, y int) int {
 return x + y
}

func add(x, y int) int {
 return x + y
}

func main() {
 fmt.Println(add(42, 13))
}
```

## Multiple results

A function can return any number of results.

The swap function returns two strings.

```go
package main

import "fmt"

func swap(x, y string) (string, string) {
 return y, x
}

func main() {
 a, b := swap("hello", "world")
 fmt.Println(a, b)
}
```

## Named return values

Go's return values may be named. If so, they are treated as variables defined at the top of the function.

These names should be used to document the meaning of the return values.

A return statement without arguments returns the named return values. This is known as a "naked" return.

Naked return statements should be used only in short functions, as with the example shown here. They can harm readability in longer functions.

```go
package main

import "fmt"

func split(sum int) (x, y int) {
 x = sum * 4 / 9
 y = sum - x
 return
}

func main() {
 fmt.Println(split(17))
}
```

## Function Values

Functions are values too. They can be passed around just like other values.

Function values may be used as function arguments and return values.

```go
package main

import (
 "fmt"
 "math"
)

func compute(fn func(float64, float64) float64) float64 {
 return fn(3, 4)
}

func main() {
 hypot := func(x, y float64) float64 {
  return math.Sqrt(x*x + y*y)
 }
 fmt.Println(hypot(5, 12))

 fmt.Println(compute(hypot))
 fmt.Println(compute(math.Pow))
}
```

## Function closures

Go functions may be closures.
A closure is a function value that references variables from outside its body.
The function may access and assign to the referenced variables; in this sense the function is "bound" to the variables.

```go
package main

import "fmt"

func adder() func(int) int {
 sum := 0
 return func(x int) int {
  sum += x
  return sum
 }
}

func main() {
 pos, neg := adder(), adder()
 for i := 0; i < 10; i++ {
  fmt.Println(
   pos(i),
   neg(-2*i),
  )
 }
}
```
