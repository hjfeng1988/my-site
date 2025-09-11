# Basic Type

## Basic Type

```
package main

import "fmt"

func main() {
	var a bool
	var b string
	var c int
	var d float64
	var e byte // 表示 ASCII 字符
	var f rune // 表示 Unicode 字符

	fmt.Println(a, b, c, d, e, f)
	fmt.Printf("%T,%T,%T,%T,%T,%T\n", a, b, c, d, e, f)
	e = 'a' // 单引号表示字符，双引号表示字符串
	f = 97
	fmt.Printf("%c,%d\n", e, e)
	fmt.Printf("%c,%d\n", f, f)
}
```

输出
```
false  0 0 0 0
bool,string,int,float64,uint8,int32
a,97
a,97
```