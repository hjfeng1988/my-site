## Composite Type

声明格式
```
array
var 变量名 [元素数量]元素类型
slice
var 变量名 []元素类型
map
var 变量名 map[键类型]值类型

数组是值类型 切片是引用类型 map是引用类型
```

示例
```
package main

import (
	"fmt"
	"reflect"
)

func main() {
	var array1 [3]int = [3]int{1, 2, 3}
	array2 := [3]string{"a", "b", "c"}
	var slice1 []int = []int{4, 5, 6}
	slice2 := []string{"e", "f", "g"}
	var map1 map[string]int = map[string]int{"x": 1}
	map2 := map[int]string{1: "y"}

	fmt.Printf("%v %v %T %T\n", array1, array2, array1, array2)
	fmt.Printf("%v %v %T %T\n", slice1, slice2, slice1, slice2)
	fmt.Printf("%v %v %T %T\n", map1, map2, map1, map2)

	fmt.Println("-----")
	tArray1 := reflect.TypeOf(array1)
	tArray2 := reflect.TypeOf(array2)
	tSlice1 := reflect.TypeOf(slice1)
	tSlice2 := reflect.TypeOf(slice2)
	tMap1 := reflect.TypeOf(map1)
	tMap2 := reflect.TypeOf(map2)

	fmt.Printf("kind=%s, type=%s\n", tArray1.Kind(), tArray1.String())
	fmt.Printf("kind=%s, type=%s\n", tArray2.Kind(), tArray2.String())
	fmt.Printf("kind=%s, type=%s\n", tSlice1.Kind(), tSlice1.String())
	fmt.Printf("kind=%s, type=%s\n", tSlice2.Kind(), tSlice2.String())
	fmt.Printf("kind=%s, type=%s\n", tMap1.Kind(), tMap1.String())
	fmt.Printf("kind=%s, type=%s\n", tMap2.Kind(), tMap2.String())
}
```

输出
```
[1 2 3] [a b c] [3]int [3]string
[4 5 6] [e f g] []int []string
map[x:1] map[1:y] map[string]int map[int]string
-----
kind=array, type=[3]int
kind=array, type=[3]string
kind=slice, type=[]int
kind=slice, type=[]string
kind=map, type=map[string]int
kind=map, type=map[int]string
```