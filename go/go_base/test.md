​									go 单元测试和性能测试

[TOC]

##### 1.单元测试

`代码示例`

```go
fun TestA(t *testing.T){//A 为待测试的方法名称
	expected:="a"
	actual:=a()
	if ""!=a(){
		t.Errof("want to be %q actual get %q",expected,actual)
	}
}
// 运行 ： go test -run=A ./other
1. -run=A|B  匹配要运行的函数名称（模糊匹配），多个名称用 | 隔开
2. ./other  待测试文件/目录 相对当前命令的位置

```

> 1. 方法名必须是 Test 开头  
> 2. 参数 必须是 *testing.T

###### 1.1 单元测试覆盖率分析

``` 
1. go test -run=A|B -coverprofile=c.out  ./other --> 生成覆盖率分析文件
2. go tool cover -html=c.out  //在浏览器显示 覆盖率结构
```



##### 2.benchTest  性能测试

`code`

```go
func BenchmarkA(t *testing.B){
	for i:=0;i<t.N;i++{
		A()
	}
}
//:运行
 go test -run=None -bench=A -benchmem ./other
1. -run=None 不运行普通的测试
2. -bench=A 运行匹配方法名A 的测试方法
3. -benchmem 显示 内存占用结果
4. ./other 待测试文件/目录  相对当前命令的位置
```

> 1. 方法名 必须Benchmark 开头
> 2. 参数必须 *testing.B



###### 2.1 性能分析

```
go test -run=None -bench=A -benchmem -cpuprofile=cpu.log ./



go tool pprof -text -nodecount=10 ./other.test cpu.log
```

