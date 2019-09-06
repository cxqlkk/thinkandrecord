#### channel之close()

channel 作为goroutine 通信媒介，分为有缓冲和无缓冲的channel,

> 关于无缓冲和缓冲为1 的区别
>
> 无缓冲： 当朝channel 发送一个值，当前goroutine 立即阻塞，直到其他goroutine 将值接受
>
> 缓冲为1：向channel 发送一个值 ，不阻塞，发送第二个值阻塞



由于channel 有时候会在一个或多个 goroutine,接受多个值，那么在某个goroutine 会以遍历的形式将值取出

```
ch:=make(chan int) //此处是否缓冲无所谓
go func(){
	ch<-1
	time.Sleep(time.Second*1)
	ch<-1
	...//上述类似代码
}

for{
	fmt.Println(<-ch)
}
或者 for m :range ch{
	fmt.Println(m)
}

```



但是有个问题，当不再需要 向 ch 里发送数据时候，遍历接受ch 值的goroutine 阻塞在遍历的逻辑中，等待ch的值，后面的逻辑无法执行了，怎么办呢，标准库提供了一个内置的Close() 用来关闭channel,当channel 最后一个值被接受，channel 会输出0，不再阻塞，那么接受的下游逻辑就可以跳出循环

```
go func(){
	//ch<-1
	Close(ch)//关闭
}
//对于 for{}
for{
	v,status:=<-ch //当channel 关闭后， v，status= 0，false
	if status!=false{
		fmt.println(v)
	}
}

// 对于使用 range遍历的  不用改动，close()后自动跳出逻辑，不再阻塞
for m :=range ch{
	fmt.Println(m)
}
```



> 及时的关闭 Channel, 可以不阻塞下游逻辑，对于 for range, 都不用改逻辑，for{} 需要做点判断