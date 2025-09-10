# Constant

## const

```
package main

import "fmt"

const pi = 3.1415
const e = 2.7

func main() {
    // e = 2.8 // 常量不能修改
	fmt.Println(pi, e)
}
```
## iota

```
package main

import "fmt"

const (
	Spring = iota // 0
	Summer        // 1
	Autumn        // 2
	Winter        // 3
)

func main() {
	fmt.Println(Spring, Summer, Autumn, Winter)

	const (
		n1 = iota // 0
		n2        // 1
		n3 = 100
		n4 = iota // 3
	)
	const n5 = iota // 0
	fmt.Println(n1, n2, n3, n4, n5)
}
```