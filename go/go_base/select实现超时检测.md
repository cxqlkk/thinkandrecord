#### select 实现超时检测

必要的超时检测和处理是必须的，某项任务如果出现不符合预期的运行时间，我们需要做其他处理，select 配合 time.After(time.Duration) 可以实现

```
//
ch:=make(chan interface{})
go func(){
	time.sleep(time.Second*3)// 模拟3秒返回机制
	ch<- 99// 任意返回结果
}()

select {
	case <-ch:
		fmt.Println("work well and return")
	case time.After(time.Second*4) //4秒 后执行
		fmt.Println("超时")
}



```



> 关于time.After(time.Second*4) 是从什么时候 作为开始作为起始时间的
>
> >  ： 是从  select 开始执行的时候