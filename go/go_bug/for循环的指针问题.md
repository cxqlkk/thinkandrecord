
	mp:=[]string{"1","2","3","4"}
	for _,v:=range mp{
		fmt.Printf("%p\n",&v)
	}

> 输出：0xc000064220
0xc000064220
0xc000064220


`for 循环临时变量的地址值是一样的`