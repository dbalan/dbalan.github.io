---
layout: post
title: "Notes on cgo"
date: 2015-03-29 00:28
comments: true
categories:
- golang
- c
---

## Referencing c from go.

### Basic operation

import "C" imports the C namespace into go, the comment just above this statement is treated as C.

```c
/*
 #include "add.h"
 */
 import "C"
```
Everything you exported from c library is available in the C namespace.

```go
func main() {
   fmt.Println(
     C.add_two_numbers(3,4)
   )
}
```

Building code is as easy as `go build`

Accessing standard types are easy as `C.char`, `C.int`. For complex types, prepend the type name with an underscore at end – e.g `C.struct_stat`.

### Pointers and memory operations

Go provides an `unsafe` module. Go’s GC cannot manage the memory allocated in C code, you should call `C.free(unsafe.Pointer)` (`free` is defined in `<stdlib.h>` ensure that this library is imported) to deallocate.
There are some special functions which convert Go types to C types and vice versa. (lifted from cgo documentation)
```go
// Go string to C string
// The C string is allocated in the C heap using malloc.
// It is the caller's responsibility to arrange for it to be
// freed, such as by calling C.free (be sure to include stdlib.h
// if C.free is needed).
func C.CString(string) *C.char

// C string to Go string
func C.GoString(*C.char) string

// C string, length to Go string
func C.GoStringN(*C.char, C.int) string

// C pointer, length to Go []byte
func C.GoBytes(unsafe.Pointer, C.int) []byte
```

### Accessing complex objects

Accessing structs from Go
```go
/*
struct person {
int age;
*/
// this can be used in go as
var p C.struct_person
p.age = 23
```

You can also pass pointers

```go
C.function_accepts_ptr_to_struct(&p)
```

Accessing Unions : No native counterpart, instead of converting it to a type, go treats them as a block of memory represented as byte array. Accessing data is done by casting unsafe.Pointer

```go
/*
union quant {
  float weight;
  int count;
};
*/

var q C.union_quant
ptr := (*float32)(unsafe.Pointer(&q))
*ptr = 3.14
```

## Extra goodies

### Compiler Flags
Compiler flags can be set using the `#cgo` directive. (`CFLAGS`, `LDFLAGS` etc)

```go
/*
#cgo: LDFLAGS: -lmath
#include <math.h>
*/
import "C"
```

### Restricting building
In many cases using cgo breaks the portability of your app, use build constraints to specify compatibility in source. Build constraints are comments which begin with

```go
// +build
```
Now, build comment must appear before package clause and should be followed by a blank line To restrict building just to Linux with cgo,

```go
// +build linux,cgo !darwin

package main
```

These are evaluated as `OR` of each constraint so the above line becomes `(linux AND cgo) OR (NOT darwin)`, also multiple build tags can be embedded in file.

There are other methods to restrict builds, see references.

## Reference

 - [Link to example code gist](https://gist.github.com/dbalan/ace29f0c43638ee4f81d)
 - [cgo Talk by Rajesh Ramachandran (Gophercon India)](https://www.youtube.com/watch?v=oeEVtyypYPg)
 - [Conditional compilation with go build](http://dave.cheney.net/2013/10/12/how-to-use-conditional-compilation-with-the-go-build-tool)
 - [cgo compiler directives](http://golang.org/cmd/cgo/)

