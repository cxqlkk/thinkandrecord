type 常用的方式

```
type A int 

func (a *A)say(){	
	fmt.Println("aaa")
}



type B A

var b B =B(1) 
b.say()// error 

b=A(b) //error 报错。。
b1:=A(b)// ok 必须重新命名变量名
b1.say()//error cannot take the address of b1   
((*A)(&b1)).say()//pass**************


type M =A //第一次见到也很吃惊
var m M = M(1)
m.say()//output: aaa









```

