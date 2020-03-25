# for 循环注意点

```
type student struct {
	Name string
	Age  int
}

func TestStudentA(t *testing.T) {
	m := make(map[string]*student)
	stus := []student{
		{Name: "zhou", Age: 24},
		{Name: "li", Age: 23},
		{Name: "wang", Age: 22},
	}
	for _, stu := range stus {
		m[stu.Name] = &stu
		fmt.Printf("%p\n",&stu)
	}
	//for k,v:=range m{
	//	fmt.Println(k,*v)
	//}
}

```
> 神奇的是 循环中stu 始终是一个地址，导致了map 里的值都是指向相同的地址