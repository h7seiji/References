# Go

<https://go.dev/doc/>

## Commands

`go mod init example/hello`

`go run .`

`go mod tidy`

`go mod edit -replace example.com/greetings=../greetings`

## Exported names

In Go, a function whose name starts with a capital letter can be called by a function not in the same package.
This is known in Go as an exported name.

## Operators

### Initialize and assign variable

`message := fmt.Sprintf("Hi, %v. Welcome!", name)`

## Data types

### Slices

<https://go.dev/blog/slices-intro>
