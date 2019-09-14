#### go 变量声明初始化

##### go 变量声明和初始化的方式如下

```
type people struct{
	name string
}

一、var p people

二、var p:=people{} 
//people{"xm"} 
//people{name:"xm"}--> 如果有多个成员，但只初始化其中部分，需要加上字段名称

三、 p:=people{}

四、 p:=new(people) == &people{}

```

##### 说下注意的地方

var p people   这种声明方式，p可以直接调用people的方法

空结构体的内存大小为1 unsafe.Sizeof(struct{})-->4

所以作为通道信息比较节省内存