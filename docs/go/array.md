# Array

## 数组的初始化
```
func main() {
	// 指定长度和初始化值
	// var array1 [3]int = [3]int{1, 2, 3}
	var array1 = [3]int{1, 2, 3}

	// 自动推断长度
	array2 := [...]int{4, 5, 6}

	// 部分初始化
	array3 := [5]int{1: 1, 2: 2}

	fmt.Printf("%T %v\n", array1, array1) // [3]int [1 2 3]
	fmt.Printf("%T %v\n", array2, array2) // [3]int [4 5 6]
	fmt.Printf("%T %v\n", array3, array3) // [5]int [0 1 2 0 0]
}
```

## 数组的遍历
```
func main() {
	var array4 = [...]string{"beijing", "shanghai", "guangzhou", "shenzhen"}
	// 传统for遍历
	for i := 0; i < len(array4); i++ {
		fmt.Println(i, array4[i])
	}

	// for range遍历
	for i, city := range array4 {
		fmt.Println(i, city)
	}
}
```

## 二维数组

```
func main() {
	array5 := [...][2]string{
		{"beijing", "hebei"},
		{"shanghai", "jiangsu"},
		{"guangzhou", "guangdong"},
		{"shenzhen", "guangdong"},
	}
	fmt.Println(array5)
	// [[beijing bj] [shanghai sh] [guangzhou gz] [shenzhen sz]]
}
```

## 数组是值类型
```
func main() {
	array6 := [3]int{7, 8, 9}
	array7 := array6
	array7[0] = 0
	fmt.Println(array6) // [7 8 9]
	fmt.Println(array7) // [0 8 9]
}
```
