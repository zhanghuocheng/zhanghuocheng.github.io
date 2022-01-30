go基础面试题

###  1 数据结构

####  1 nil 切片和空切片的区别

```
nil 切片 指向的空地址，空切片执行的zero数组 ，所有的空切片都指向zero数组 
```

```go


func main() {

 var s1 []int
 s2 := make([]int,0)
 s4 := make([]int,0)
 
 fmt.Printf("s1 pointer:%+v, s2 pointer:%+v, s4 pointer:%+v, \n", *(*reflect.SliceHeader)(unsafe.Pointer(&s1)),*(*reflect.SliceHeader)(unsafe.Pointer(&s2)),*(*reflect.SliceHeader)(unsafe.Pointer(&s4)))
 fmt.Printf("%v\n", (*(*reflect.SliceHeader)(unsafe.Pointer(&s1))).Data==(*(*reflect.SliceHeader)(unsafe.Pointer(&s2))).Data)
 fmt.Printf("%v\n", (*(*reflect.SliceHeader)(unsafe.Pointer(&s2))).Data==(*(*reflect.SliceHeader)(unsafe.Pointer(&s4))).Data)
}
```

#### 2 避免内存拷贝

强制类型转换都会发生内存拷贝

怎么避免 已字符串转为例--强转底层结构

```go
func main() {
 a :="aaa"
 ssh := *(*reflect.StringHeader)(unsafe.Pointer(&a))
 b := *(*[]byte)(unsafe.Pointer(&ssh))  
 fmt.Printf("%v",b)
}

字符串底层结构
type StringHeader struct {
 Data uintptr
 Len  int
}

切面底层结构

type SliceHeader struct {
 Data uintptr
 Len  int
 Cap  int
}
```

#### 3 go 中文字符数组 字符串反转

rune是int32 2^21次 可以存下任意字符

byte -128-127

```go
func main() {
	src := "你好abc啊哈哈"
	dst := reverse([]rune(src))
	fmt.Printf("%v\n", string(dst))
}

func reverse(runes []rune) string {
	length := len(runes)
	for i := 0; i < len(runes)/2; i++ {
		runes[i], runes[length-1-i] = runes[length-1-i], runes[i]
	}
	return string(runes)
}
```

#### 4 json 加不加tag   

```
如果变量首字母小写，则为private。无论如何不能转，因为取不到反射信息。
如果变量首字母大写，则为public。
不加tag，可以正常转为json里的字段，json内字段名跟结构体内字段原名一致。
加了tag，从struct转json的时候，json的字段名就是tag里的字段名，原字段名已经没用。
```

```go
type J struct {
    a string             //小写无tag
    b string `json:"B"`  //小写+tag
    C string             //大写无tag
    D string `json:"DD"` //大写+tag
}
func main() {
    j := J {
      a: "1",
      b: "2",
      C: "3",
      D: "4",
    }
    fmt.Printf("转为json前j结构体的内容 = %+v\n", j)
    jsonInfo, _ := json.Marshal(j)
    fmt.Printf("转为json后的内容 = %+v\n", string(jsonInfo))
}
//
转为json前j结构体的内容 = {a:1 b:2 C:3 D:4}
转为json后的内容 = {"C":"3","DD":"4"}
```

#### 5 为啥反射不能去除json包小写字母开头的变量

```
源码在解析是 不是public的变量故意跳过，不解析
```

#### 6 map不初始化，取值没问题，赋值会painc

```go
func main() {

	var myMap map[int]int
	myMap1 := map[int]int{}

	if p, ok := myMap[1]; ok {
		fmt.Printf("p=%+v", p)
	} else {
		fmt.Printf("p=%+v", p)
	}
	fmt.Printf("myMap=%+v，myMap1=%+v", len(myMap), len(myMap1))
	
	// set
	myMap[1] = 1
}
//
p=0myMap=0，myMap1=0  panic: assignment to entry in nil map
goroutine 1 [running]:
main.main()
        /Users/huocheng/Desktop/go-suanfa/dayOne/leetcode_day_1.go:14 +0xdc
```



### 2 流程控制





