### map-再学golang
1. map 创建
2. map 增删改查
3. 小技巧
   

#### 1. map 创建
##### 1.1 简单map 创建
```
// 方式1
 mp:=map[string]string{}

 //方式2
 mp:=make(map[string]string)

```
##### 1.2 结构体中map

```
type Class struct{
    Student map[string]interface{}{}
}

//
c1 :=Class{}
c.Student["a"]="ss" //报错



```
