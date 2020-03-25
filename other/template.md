### template 使用总结
在公司实战用了几次的template ,功效还是蛮大的，但是缺发一个全面的学习，每次都要重新百度，现在来总结一下

#### 1. 创建模板对象
有两种方式穿件模板对象
1. template.New()
> 用来从字符串载入模板
> 通常和 Execute()联合使用

```

	strtmp:=`{{.Age}}`
	t,_:=template.New("").Parse(strtmp)
	t.Execute(os.Stdout,map[string]string{"Age":"33"})

```




1. temp.ParseFile()

