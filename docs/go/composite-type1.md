## Composite Type

## 声明格式
```
array
var 变量名 [元素数量]元素类型
slice
var 变量名 []元素类型
map
var 变量名 map[键类型]值类型

数组是值类型 切片是引用类型 map是引用类型
```

## 示例
```
package main

import (
	"fmt"
	"reflect"
)

func main() {
	var array [3]int
	var slice []int
	var m map[string]int

	fmt.Printf("%v %T\n", array, array)
	fmt.Printf("%v %T\n", slice, slice)
	fmt.Printf("%v %T\n", m, m)

	fmt.Println("-----")
	tArray := reflect.TypeOf(array)
	tSline := reflect.TypeOf(slice)
	tMap := reflect.TypeOf(m)

	fmt.Printf("kind=%s, type=%s\n", tArray.Kind(), tArray.String())
	fmt.Printf("kind=%s, type=%s\n", tSline.Kind(), tSline.String())
	fmt.Printf("kind=%s, type=%s\n", tMap.Kind(), tMap.String())
}
```

## 输出
```
[0 0 0] [3]int
[] []int
map[] map[string]int
-----
kind=array, type=[3]int
kind=slice, type=[]int
kind=map, type=map[string]int
```