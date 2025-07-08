# Flow Control

## For

Go has only one looping construct, the for loop.

The basic for loop has three components separated by semicolons:

- the init statement: executed before the first iteration
- the condition expression: evaluated before every iteration
- the post statement: executed at the end of every iteration

Note: Unlike other languages like C, Java, or JavaScript there are no parentheses surrounding the three components of the for statement and the braces { } are always required.

```go
package main

import "fmt"

func main() {
 sum := 0
 for i := 0; i < 10; i++ {
  sum += i
 }
 fmt.Println(sum)
}

// The init and post statements are optional (works as "while")
func main() {
 sum := 1
 for sum < 1000 {
  sum += sum
 }
 fmt.Println(sum)
}
```

## If

Go's if statements are like its for loops; the expression need not be surrounded by parentheses ( ) but the braces { } are required.

Variables declared by the statement are only in scope until the end of the if.

```go
package main

import (
 "fmt"
 "math"
)

func sqrt(x float64) string {
 if x < 0 {
  return sqrt(-x) + "i"
 } else {
  fmt.Printf("%g >= %g\n", v, lim)
 }
 return fmt.Sprint(math.Sqrt(x))
}

func main() {
 fmt.Println(sqrt(2), sqrt(-4))
}

// Like for, the if statement can start with a short statement to execute before the condition.

func pow(x, n, lim float64) float64 {
 if v := math.Pow(x, n); v < lim {
  return v
 }
 return lim
}
```

## Switch

Go's switch is like the one in C, C++, Java, JavaScript, and PHP, except that Go only runs the selected case, not all the cases that follow.
In effect, the break statement that is needed at the end of each case in those languages is provided automatically in Go.
Another important difference is that Go's switch cases need not be constants, and the values involved need not be integers.

```go
package main

import (
 "fmt"
 "runtime"
)

func main() {
 fmt.Print("Go runs on ")
 switch os := runtime.GOOS; os {
 case "darwin":
  fmt.Println("macOS.")
 case "linux":
  fmt.Println("Linux.")
 default:
  // freebsd, openbsd,
  // plan9, windows...
  fmt.Printf("%s.\n", os)
 }
}
```

### Switch with no condition

Switch without a condition is the same as switch true.

This construct can be a clean way to write long if-then-else chains.

```go
package main

import (
 "fmt"
 "time"
)

func main() {
 t := time.Now()
 switch {
 case t.Hour() < 12:
  fmt.Println("Good morning!")
 case t.Hour() < 17:
  fmt.Println("Good afternoon.")
 default:
  fmt.Println("Good evening.")
 }
}
```

## Defer

A defer statement defers the execution of a function until the surrounding function returns.

The deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns.

Deferred function calls are pushed onto a stack. When a function returns, its deferred calls are executed in last-in-first-out order.

```go
package main

import "fmt"

func main() {
 defer fmt.Println("world")

 fmt.Println("hello")
}
```
