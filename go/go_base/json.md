#### go  json 序列化和反序列化



##### 1. json 序列化

```go
type person struct{
	Name string `json:"name"`
	Age int `json:"age"`
}
var p = person{"xm",20}
bts,_:=json.Marshal(p)
fmt.println(string(bts))

```

`注意：字段名一定要大写（导出字段）`

##### 2. json 反序列化

```go
type personArr []struct{
	Address string `json:"address"`
	UserName string `json:"username"`
}

str:="[{\"address\":\"北京\",\"username\":\"kongyixueyuan\"}]"
	var p personArr
	json.Unmarshal([]byte(str),&p)
	for _,m:=range p{
		fmt.Println(m.Address,m.UserName)
	}
```



##### 3 json 反序列化工具

> 如果给定一个复杂的数据，手工书写一个待解析的结构体，容易出错（亲身体会） ，
>
> https://mholt.github.io/json-to-go/可以将给定的json 数据 ，给出需要的结构体，超级好的工具