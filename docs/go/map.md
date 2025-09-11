# Map

## 声明和初始化
```
func main() {
	// 声明、初始化、赋值分三步
	var map1 map[string]int
	// map1["one"] = 1 // 此时不能直接使用
	map1 = make(map[string]int)
	map1["one"] = 1

	// 声明+初始化、赋值分两步
	var map2 = make(map[string]int)
	map2["two"] = 2

	// 声明+初始化+赋值
	map3 := map[string]int{"three": 3}

	fmt.Printf("%T %v\n", map1, map1) // map[string]int map[one:1]
	fmt.Printf("%T %v\n", map2, map2) // map[string]int map[two:2]
	fmt.Printf("%T %v\n", map3, map3) // map[string]int map[three:3]
}
```

## 判断map中是否存在某个key
```
func main(){
    map4 := map[string]int{
		"one":   1,
		"two":   2,
		"three": 3,
	}

	v, ok := map4["one"]
	if ok {
		fmt.Println(v)
	} else {
		fmt.Println("the key is not exist")
	}
}
```

## map是引用类型
```
func main(){
	fmt.Println(map4) // map[one:1 three:3 two:2]
	map5 := map4
	map5["one"] = 4
	fmt.Println(map4) // map[one:4 three:3 two:2]
}
```

## 元素为map类型的切片
```
func main(){
    var mapSlice = make([]map[string]string, 3)
	fmt.Println(mapSlice) // [map[] map[] map[]]
	mapSlice[0] = make(map[string]string)
	mapSlice[0]["name"] = "mike"
	mapSlice[0]["sex"] = "male"
	mapSlice[0]["city"] = "beijing"
	fmt.Println(mapSlice) // [map[city:beijing name:mike sex:male] map[] map[]]
}
```

## 值为切片类型的map

```
func main(){
    var sliceMap = make(map[string][]string)
	sliceMap["chinese"] = []string{"beijing", "shanghai"}
	sliceMap["japanese"] = []string{"tokyo", "osaka"}
	fmt.Println(sliceMap) // map[chinese:[beijing shanghai] japanese:[tokyo osaka]]
}
```