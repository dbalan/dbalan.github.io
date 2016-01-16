---
layout: post
title: "go: `:=` operator causes accidental shadowing"
date: 2016-01-14 21:13
comments: true
categories:
  - go
---

Go provides `:=` operator to make declaring variables easier. It is a [shorthand to declare and set a value of a variable](https://golang.org/ref/spec#Short_variable_declarations). for example,

```go
var x int
x = 42
```
can be written as

```go
x := 42
```
But if not careful, this can accidently shadow variable bindings. Let's look at the fictitious piece of code.

```go
package main

import "fmt"


func fictitiousFunc() (int, error) {
	return 42, nil
}

func main() {
	x := 10;
	x, err := fictitiousFunc()
    if err != nil {
		fmt.Println("I'll never print")
    }
	fmt.Println("value of x: ", x)
}
```
This produces following output

```
value of x:  42
```
While, this following piece of code will fail to compile

```go
package main

import "fmt"

func fictitiousFunc() (int, error) {
    return 42, nil
}

func main() {
    x := 10
    // replace :=
    var x int
    var err error
    x, err = fictitiousFunc()
    if err != nil {
        fmt.Println("I'll never print") 
    }
    fmt.Println("value of x: ", x)
}

```
output:
```
prog.go:12: x redeclared in this block
    previous declaration at prog.go:10
```
So we can see that the operator is somewhat intelligent, and does not redeclare the variables. 

Now what if we push it down a scope? See the following code

```go
package main

import "fmt"


func fictitiousFunc() (int, error) {
	return 42, nil
}

func main() {
	someCondition := true
	
	x := -1;
	
	if someCondition {
		x, err := fictitiousFunc()
		
		if err != nil {
			fmt.Println("I'll never print")
		}
		
		fmt.Println("value of x inside: ", x)
	}
	
	fmt.Println("value x outside: ", x)
	
}
```

This produces,
```go
value of x inside:  42
value x outside:  -1
```

At line: 16, since the immediate scope (line:15-32) does not have variable `x` declared, `:=` is redeclaring the variable. a.k.a the __variable `x` gets shadowed__.

Only workaround I can think of is not to use `:=`, i.e change the code to
```go
	if someCondition {
        var err error
        x, err = fictitiousFunc()
		
		if err != nil {
			fmt.Println("I'll never print")
		}
		
		fmt.Println("value of x inside: ", x)
	}
```

If you know something better let me know.
