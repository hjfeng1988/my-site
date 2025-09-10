# Module

## 同一个项目import

### 目录结构
```
├─p1
│  │  go.mod
│  │  main.go
│  └─p2
│          p2.go
```

### p2
`p1/p2/p2.go`
```
package p2

import "fmt"

func New() {
	fmt.Println("p2.New")
}
```

### p1
`p1/go.mod`
```
module p1

go 1.24.4
```

`p1/main.go`
```
package main

import (
	"fmt"
	"p1/p2"
)

func main() {
	fmt.Println("main")
	p2.New()
}
```

### 输出
```
PS D:\git\1.go\p1> go run .\main.go
main
p2.New
p3.New
```

## 不同项目import

### 目录结构
```
├─p1
│  │  go.mod
│  │  main.go
│  └─p2
│          p2.go
└─p3
        go.mod
        p3.go
```

### p3
`p3/p3.go`
```
package p3

import "fmt"

func New() {
	fmt.Println("p3.New")
}
```
`p3/go.mod`
```
module p3

go 1.24.4
```

### p1
`p1/main.go`
```
package main

import (
	"fmt"
	"p1/p2"
	"p3"
)

func main() {
	fmt.Println("main")
	p2.New()
	p3.New()
}
```

`p1/go.mod` 使用`replace`指令
```
module p1

go 1.24.4

require "p3" v0.0.0
replace "p3" => "../p3"
```

### 输出
```
PS D:\git\1.go\p1> go run .\main.go
main
p2.New
p3.New
```