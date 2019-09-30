在[计算机科学](https://wc.yooooo.us/wiki/计算机科学)中，**反射**是指[计算机程序](https://wc.yooooo.us/wiki/计算机程序)在[运行时](https://wc.yooooo.us/wiki/运行时)（Run time）可以访问、检测和修改它本身状态或行为的一种能力。[[1\]](https://wc.yooooo.us/wiki/反射_(计算机科学)#cite_note-Forman_p8-1)用比喻来说，反射就是程序在运行的时候能够“观察”并且修改自己的行为。 （摘自维基百科）

[TOC]

#### 1.type 和value

在go 中任何数据类型都有 type 和value (value 可能为空)， 代表类型和具体的值

```go
var a int =1
fmt.Println(reflect.TypeOf(a),reflect.ValueOf(a))
//output:int  1
```

##### 1.1 type

###### 1.11 Elem()

> 有名词称为”取值“,type 和 value 都有这个方法,
>
> ```go
> value:
> // Elem returns the value that the interface v contains
> // or that the pointer v points to.
> // It panics if v's Kind is not Interface or Ptr.
> // It returns the zero Value if v is nil.
> ```
>
> ```go
> type:
> 
> // Elem returns a type's element type.
> // It panics if the type's Kind is not Array, Chan, Map, Ptr, or Slice.
> ```

```go
type people struct{
    name string
    age int
}
p1:=people{"aa",22}
p1t:=reflect.Typeof(p1)
p1v:=reflect.Valueof(p1)
fmt.Println(p1t,p1v);//people    {aa 222}

p1elev p1elet:=p1v.Ele(),p1t.Ele() //  error , 调用者必须是 Ptr 或者是上述其他类型

//
p1:=&people{"aa",22} //区别上面的是 用指针
p1t:=reflect.Typeof(p1)
p1v:=reflect.Valueof(p1)
fmt.Println(p1t,p1t.Ele()); //*people   people 
fmt.Println(p1v,p1v.Ele());//&{aa,22} {aa,22}

```

###### 1.12  structField

>可以通过如下方法获得
>
>Field(index int) structField
>
>FieldByIndex(index []int) 复合字段[]int{2,3} 索引为2 的字段的索引为3 的字段
>
>FieldByName(name string) 

>  其 包含 Name,Tag,pkg,offSet, Anonymous ,index  ,isValid
>
> Anonymous 用来判断是否是导出字段
>
> Tag `json:"sss"`  tag.lookup("json") tag.Get("json") 写框架用得到

###### 1.13 func

> ```go
> f,_:=p1t.Elem().MethodByName("Say")
> f.func.call([]reflect.Value{})
> ```

###### 1.14 转成value

reflect.New(t type) 0xaaasdf

reflect.Zero(t type)  nil

##### 2.value

###### 2.1 Elem() 同上

###### 2.2 关于Feild(index int) ...等方法

> 和type 中同名方法类似，但是返回值是Value
>
> ```go
> p1v.Ele().Field(0).interface() ->"xa" （name的值）
> 注意：如果是未导出字段 会报错
> 需要
> plv.Elem().Type().Field(0).Anonymous 判断是否是导出字段
> ```

###### 2.3 转Type

> 有的时候，需要从 value 获得Type 里的属性，比如 字段类型（structField.Type),注解（structField.Tag)
>
> 是否可导出 structField.Anonymous
>
> 结构体的名称type.Name

```
Typeof()
例子
v：=reflect.Valueof(&people{})
v.Elem().Type().Name   people
```



