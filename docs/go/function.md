# Function

## 函数基础
### 声明格式
```
func 函数名(参数 参数类型)(返回值 返回值类型) {
    函数体
}
```

### 无参无返回值函数
```
func myprint1() {
	fmt.Println("myprint")
}
```

### 有一个参数的函数
```
func myprint2(msg string) {
	fmt.Println(msg)
}
```

### 有两个参数，一个返回值的函数
```
func myprint3(a, b int) int {
	c := a + b
	return c
}
```

### 返回值命名
```
func myprint4(a, b int) (c int) {
	c = a + b
	return
}
```

### 有多个返回值的函数
```
func myprint5(x, y string) (string, string) {
	return y, x
}
```

### 不定参数的函数
```
func myprint6(x ...int) {
	fmt.Println(x)
}
```

## 函数顺序
```
func main() {
	funca(3)
	fmt.Println("main")
}

func funcc(c int) {
	fmt.Println("c =", c)
}

func funcb(b int) {
	funcc(b - 1)
	fmt.Println("b =", b)
}

func funca(a int) {
	funcb(a - 1)
	fmt.Println("a =", a)
}
```

输出
```
c = 1
b = 2
a = 3
main
```

## 递归函数
```
func main() {
	fmt.Println("1加到100的和是:", mysum(100))
}

func mysum(i int) int {
	if i == 1 {
		return 1
	} else {
		return i + mysum(i-1)
	}
}
```

## 高阶函数
```
func main() {
	rt1 := calc(3, 4, add)
	fmt.Println(rt1)

	rt2 := calc(3, 4, sub)
	fmt.Println(rt2)
}

func calc(a, b int, op func(int, int) int) int {
	r := op(a, b)
	return r
}

// calc另一种写法
// type op func(int, int) int

// func calc(a, b int, fun op) (r int) {
// 	r = fun(a, b)
// 	return
// }


func add(a, b int) int {
	return a + b
}

func sub(a, b int) int {
	return a - b
}

```

## 匿名函数

### 声明格式
```
func(参数 参数类型)(返回值 返回值类型){
    函数体
}
```

### 通过变量调用匿名函数
```
func main() {
    add := func(x, y int) (sum int) {
		sum = x + y
		return
	}
	rt := add(10, 20)
	fmt.Println(rt)
}
```

### 自执行函数
```
func main() {
	func(x, y int) {
		fmt.Println(x + y)
	}(10, 20)
}
```

## 闭包

```
func main() {
	rt1 := test01()
	fmt.Println(rt1)
	fmt.Println(rt1)

	rt2 := test02()
	fmt.Println(rt2())
	fmt.Println(rt2())

	rt3 := test03((5))
	fmt.Println(rt3(6))

	rt4, rt5 := test04(10)
	fmt.Println(rt4(1), rt5(2))
}
func test01() int {
	var a int
	a++
	return a * a //函数调用完毕，a自动释放
}

func test02() func() int {
	var a int
	return func() int {
		a++
		return a * a
	}
}

func test03(a int) func(int) int {
	return func(b int) (c int) {
		c = a + b
		return
	}
}

func test04(base int) (func(int) int, func(int) int) {
	add := func(i int) int {
		base += i
		return base
	}

	sub := func(i int) int {
		base -= i
		return base
	}
	return add, sub
}
```

输出
```
1
1
1
4
11
11 9
```
## defer

```
func test(x int) {
	fmt.Println(100 / x) //x为0时，产生异常
}

func main() {
	defer fmt.Println("aaa")
	defer fmt.Println("bbb")
	defer test(0)
	defer fmt.Println("ccc")
}
```

输出
```
ccc
bbb
aaa
panic: runtime error: integer divide by zero
```