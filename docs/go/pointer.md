# Pointer

`&`取变量内存地址，`*`根据内存地址取值

```
func main() {
	a := 10
	b := &a
	fmt.Printf("a:%d ptr:%p\n", a, &a) // a:10 ptr:0xc00001a078
	fmt.Printf("b:%p type:%T\n", b, b) // b:0xc00001a078 type:*int
	fmt.Println(&b)                    // 0xc00000e018
	fmt.Println(*b)                    // 10
}
```

指针用new函数分配内存，make函数只用于slice、map、channel的初始化
```
func main() {
	var c *int
	// *c = 100 // 此时不能直接使用
	c = new(int)
	*c = 100
	fmt.Printf("%T %p %d\n", c, c, *c) // *int 0xc00000a130 100
}
```