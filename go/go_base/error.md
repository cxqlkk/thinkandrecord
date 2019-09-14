#### error  用法以及注意点

##### 1.Error 接口以及 自定义error

```go
//error 接口
type error interface{ 
	Error()string
}
//标准库提供的实现
type errorString struct{
	s string
}

func (e *errorString)Error()string{
	return e.s
}

//使用 errorString
func New(s string) error{
	return &errorString(s)
}

func main (){
	err:=errors.New("error")
}
//自定义error, 需要实现Error()string 即可 
```

##### 2.error 使用的注意点 -Why is my nil error value not equal to nil?

```
func errorInterface()error{
	var e *myError =nil
	if bad(){
		e=&myError{"error"}
	}
	fmt.Printf("%t",e) -->true 【1】
	return e
}

func main(){
	e:=errorInterface()
	fmt.Printf("%t",e==nil) 【2】
}
//output:false > 假设bad()==false

//按理说e应该是nil 为何【2】处为false 【1】为true 
// If we store a nil pointer of type *int inside an interface value, the inner type will be *int regardless of the value of the pointer: (T=*int, V=nil). Such an interface value will therefore be non-nil even when the pointer value V inside is nil.

//Under the covers, interfaces are implemented as two elements, a type T and a value V. V is a concrete value such as an int, struct or pointer, never an interface itself, and has type T
//接口保存两个元素 V 和 T ,作为返回值error接受了 V ->nil 但是T -> *myError ,所以不为nil
error={
	V nil
	T *myError
}

```



>  如果error 想返回空，那么直接返回 nil 最合适