# Arrays

The type [n]T is an array of n values of type T.

The expression `var a [10]int` declares a variable a as an array of ten integers.

An array's length is part of its type, so arrays cannot be resized.
This seems limiting, but don't worry; Go provides a convenient way of working with arrays.

```go
package main

import "fmt"

func main() {
 var a [2]string
 a[0] = "Hello"
 a[1] = "World"
 fmt.Println(a[0], a[1])
 fmt.Println(a)

 primes := [6]int{2, 3, 5, 7, 11, 13}
 fmt.Println(primes)
}
```

## Slices

An array has a fixed size.
A slice, on the other hand, is a dynamically-sized, flexible view into the elements of an array.
In practice, slices are much more common than arrays.

The type []T is a slice with elements of type T.

A slice is formed by specifying two indices, a low and high bound, separated by a colon:

`a[low : high]`

This selects a half-open range which includes the first element, but excludes the last one.

The following expression creates a slice which includes elements 1 through 3 of a:

`a[1:4]`

```go
package main

import "fmt"

func main() {
 primes := [6]int{2, 3, 5, 7, 11, 13}

 var s []int = primes[1:4]
 fmt.Println(s)
}
```

Slices are like references to arrays

A slice does not store any data, it just describes a section of an underlying array.

Changing the elements of a slice modifies the corresponding elements of its underlying array.

Other slices that share the same underlying array will see those changes.

### Slice literals

A slice literal is like an array literal without the length.

This is an array literal:

```go
[3]bool{true, true, false}
```

And this creates the same array as above, then builds a slice that references it:

```go
[]bool{true, true, false}
```

### Slice defaults

When slicing, you may omit the high or low bounds to use their defaults instead.

The default is zero for the low bound and the length of the slice for the high bound.

For the array

```go
var a [10]int
```

these slice expressions are equivalent:

```go
a[0:10]
a[:10]
a[0:]
a[:]
```

### Slice length and capacity

A slice has both a length and a capacity.

The length of a slice is the number of elements it contains.

The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice.

The length and capacity of a slice s can be obtained using the expressions len(s) and cap(s).

You can extend a slice's length by re-slicing it, provided it has sufficient capacity.

### Nil slices

The zero value of a slice is nil.

A nil slice has a length and capacity of 0 and has no underlying array.

### Creating a slice with make

Slices can be created with the built-in make function; this is how you create dynamically-sized arrays.

The make function allocates a zeroed array and returns a slice that refers to that array:

```go
a := make([]int, 5)  // len(a)=5
```

To specify a capacity, pass a third argument to make:

```go
b := make([]int, 0, 5) // len(b)=0, cap(b)=5

b = b[:cap(b)] // len(b)=5, cap(b)=5
b = b[1:]      // len(b)=4, cap(b)=4
```

### Appending to a slice

It is common to append new elements to a slice, and so Go provides a built-in append function.

```go
func append(s []T, vs ...T) []T
```

The first parameter s of append is a slice of type T, and the rest are T values to append to the slice.

The resulting value of append is a slice containing all the elements of the original slice plus the provided values.

If the backing array of s is too small to fit all the given values a bigger array will be allocated. The returned slice will point to the newly allocated array.

```go
package main

import "fmt"

func main() {
 var s []int
 printSlice(s)

 // append works on nil slices.
 s = append(s, 0)
 printSlice(s)

 // The slice grows as needed.
 s = append(s, 1)
 printSlice(s)

 // We can add more than one element at a time.
 s = append(s, 2, 3, 4)
 printSlice(s)
}

func printSlice(s []int) {
 fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}
```

## Range

The range form of the for loop iterates over a slice or map.

When ranging over a slice, two values are returned for each iteration. The first is the index, and the second is a copy of the element at that index.

```go
package main

import "fmt"

var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}

func main() {
 for i, v := range pow {
  fmt.Printf("2**%d = %d\n", i, v)
 }
}
```

You can skip the index or value by assigning to _.

```go
for i, _ := range pow
for _, value := range pow
```

If you only want the index, you can omit the second variable.

```go
for i := range pow
```
