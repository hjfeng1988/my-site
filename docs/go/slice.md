# Slice

## 声明和初始化
```
func main() {
	// 声明、初始化、赋值分三步
	var slice1 []int
	// slice1[0] = 1 // 此时不能直接使用
	slice1 = make([]int, 3)
	slice1[0] = 1

	// 声明+初始化、赋值分两步
	var slice2 = make([]int, 3, 5)
	slice2[0] = 1

	// 声明+初始化+赋值
	slice3 := []int{1, 2, 3}

	// 通过数组创建
	arr := [5]int{1, 2, 3, 4, 5}
	slice4 := arr[1:4]

	fmt.Printf("%T %v\n", slice1, slice1) // []int [1 0 0]
	fmt.Printf("%T %v\n", slice2, slice2) // []int [1 0 0]
	fmt.Printf("%T %v\n", slice3, slice3) // []int [1 2 3]
	fmt.Printf("%T %v\n", slice4, slice4) // []int [2 3 4]
}
```

## 切片的本质
切片的本质就是对底层数组的封装，它包含了三个信息：底层数组的指针、切片的长度（len）和切片的容量（cap）
```
func main() {
	// 声明、初始化、赋值分三步
	var slice1 []int
	// slice1[0] = 1 // 此时不能直接使用
	slice1 = make([]int, 3)
	slice1[0] = 1

	// 声明+初始化、赋值分两步
	var slice2 = make([]int, 3, 5)
	slice2[0] = 1

	// 声明+初始化+赋值
	slice3 := []int{1, 2, 3}

	// 通过数组创建
	arr := [5]int{1, 2, 3, 4, 5}
	slice4 := arr[1:4]

	fmt.Println(slice1, len(slice1), cap(slice1)) // [1 0 0] 3 3
	fmt.Println(slice2, len(slice2), cap(slice2)) // [1 0 0] 3 5
	fmt.Println(slice3, len(slice3), cap(slice3)) // [1 2 3] 3 3
	fmt.Println(slice4, len(slice4), cap(slice4)) // [2 3 4] 3 4
}

```

## 切片是引用类型
```
func main() {
    slice4 := []int{7, 8, 9}
	slice5 := slice4
	slice5[0] = 0
	fmt.Println(slice4) // [0 8 9]
	fmt.Println(slice5) // [0 8 9]
}
```

## 切片添加元素
```
func main() {
	slice6 := []int{1, 2, 3}
	slice6 = append(slice6, 4, 5, 6)
	fmt.Println(slice6) // [1 2 3 4 5 6]
}
```
