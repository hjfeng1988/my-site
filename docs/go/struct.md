# Struct

## 声明格式
```
type 类型名 struct {
    字段名 字段类型
    字段名 字段类型
    ...
}
```

## 结构体实例化
```
package main

import "fmt"

type Student struct {
	name string
	age  int
	city string
}

func main() {
	// 方式1
	var s1 Student
	s1 = Student{
		name: "mike",
		age:  18,
		city: "beijing",
	}

	// 方式2
	s2 := Student{
		name: "john",
		age:  18,
		city: "shanghai",
	}

	// 方式3
	var s3 Student
	s3.name = "jack"
	s3.age = 18
	s3.city = "guangzhou"

	fmt.Println(s1) // {mike 18 beijing}
	fmt.Println(s2) // {john 18 shanghai}
	fmt.Println(s3) // {jack 18 guangzhou}
}
```

## 匿名结构体
```
func main() {
	var s4 struct {
		name string
		age  int
		city string
	}
	s4.name = "rose"
	s4.age = 18
	s4.city = "shenzhen"

	fmt.Println(s4) // {rose 18 shenzhen}
}
```

## 类型定义和类型别名的区别
```
type myInt int
type newInt = int

func main() {
	var i myInt = 8
	var j int = 8
	var k newInt = 8
	fmt.Printf("%T %v\n", i, i) // main.myInt 8
	fmt.Printf("%T %v\n", j, j) // int 8
	fmt.Printf("%T %v\n", k, k) // int 8
}
```

## 结构体指针
```
func main() {
	// 方式1
	var s1 *Student
	s1 = new(Student)
	fmt.Printf("%p %T %#v\n", s1, s1, s1)

	// 方式2
	var s2 = new(Student)
	fmt.Printf("%p %T %#v\n", s2, s2, s2)

	// 方式3
	s3 := new(Student)
	fmt.Printf("%p %T %#v\n", s3, s3, s3)

	// 方式4
	s4 := &Student{} // == new(Student)
	fmt.Printf("%p %T %#v\n", s4, s4, s4)

	var s5 Student
	fmt.Printf("%T %#v\n", s5, s5)
}
```

输出
```
0xc0000221b0 *main.Student &main.Student{name:"", age:0, city:""}
0xc000022210 *main.Student &main.Student{name:"", age:0, city:""}
0xc000022270 *main.Student &main.Student{name:"", age:0, city:""}
0xc0000222d0 *main.Student &main.Student{name:"", age:0, city:""}
main.Student main.Student{name:"", age:0, city:""}
```

## 值传递和指针传递
```
type Student struct {
	name string
	age  int
	city string
}

func setAge1(s Student) {
	s.age = 30
}

func setAge2(s *Student) {
	s.age = 30
}

func main() {
	s1 := Student{"mike", 18, "beijing"}
	setAge1(s1)     // 值传递
	fmt.Println(s1) // {mike 18 beijing}
	setAge2(&s1)    // 指针传递
	fmt.Println(s1) // {mike 30 beijing}

	s2 := &Student{"john", 18, "beijing"}
	setAge1(*s2)    // 值传递
	fmt.Println(s2) // &{john 18 beijing}
	setAge2(s2)     // 指针传递
	fmt.Println(s2) // &{john 30 beijing}
}
```

## 构造函数
```
func NewStudent(name string, age int, city string) *Student {
	return &Student{
		name: name,
		age:  age,
		city: city,
	}
}

func main() {
	s1 := NewStudent("mike", 18, "beijing")
	fmt.Printf("%#v\n", s1) // &main.Student{name:"mike", age:18, city:"beijing"}
}
```

## 方法

### 声明格式
```
func (接收者变量 接收者类型) 方法名(参数列表) (返回值列表) {
	函数体
}

普通函数
func 函数名(参数列表) (返回值列表){
	函数体
}
```

### 值类型和指针类型的接收者
```
// 值类型的接收者
func (s Student) SetAge1(newAge int) {
	s.age = newAge
}

// 指针类型的接收者
func (s *Student) SetAge2(newAge int) {
	s.age = newAge
}

func main() {
	// 值类型
	s2 := Student{
		name: "john",
		age:  18,
		city: "shanghai",
	}

	// 指针类型
	s3 := &Student{
		name: "jack",
		age:  18,
		city: "guangzhou",
	}

	// 方法
	// Go 有一个 语法糖：方法调用时，编译器会自动在值和指针之间转换
	s2.SetAge1(20)          // 值调用
	fmt.Printf("%#v\n", s2) // main.Student{name:"john", age:18, city:"shanghai"}
	s2.SetAge2(30)          // 值调用，Go 会自动取地址 &s2 转换为指针调用
	fmt.Printf("%#v\n", s2) // main.Student{name:"john", age:30, city:"shanghai"}

	s3.SetAge1(20)          // 指针调用
	fmt.Printf("%#v\n", s3) // &main.Student{name:"jack", age:18, city:"guangzhou"}
	s3.SetAge2(30)          // 指针调用，Go 会自动取值 *s3 转换为值调用
	fmt.Printf("%#v\n", s3) // &main.Student{name:"jack", age:30, city:"guangzhou"}
}
```

## 嵌套结构体
```
type Adress struct {
	province string
	city     string
}

type Person1 struct {
	name   string
	gender string
	age    int
	adress Adress
}

func main() {
	p2 := Person1{
		name: "mike",
		adress: Adress{
			province: "fujian",
			city:     "fuzhou",
		},
	}
	fmt.Printf("%#v\n", p2)
}
```