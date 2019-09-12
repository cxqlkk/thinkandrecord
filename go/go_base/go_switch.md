#### go-switch 注意点



##### 1. switch 没有 break,满足条件，执行完语句自动跳出（如果没有语句直接跳出），如果想继续执行 fallthrough(不论下一个case 是否满足都执行)

```

a:=233

switch a{
	case 233:
		//fmt.Println(233） 
	case 111:
		fmt.Println(111)
}
//output:233

如果想要 继续执行
switch a{
	case 233:
		fmt.Println(233）
		fallthrough
	case 111:
		fmt.Println(111)
}
//output:
//233
//111
```

##### 2.switch 一个case 可以写多个条件，逗号隔开,满足其中一个就执行对应的语句

```
a:=111
switch a{
	case 111,222,333:
		fmt.Println(a)
}
//output:
//111
```

##### 3. switch 做类型转换判断

```
switch v:=interface.(type){
	case int:
	case string:
}
```

