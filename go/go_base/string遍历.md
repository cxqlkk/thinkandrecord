## golang  ——string 遍历

### 1. 前言

> 字符串遍历是我们工作中常用的一个手段，
>
> java 中没有切片，如果想遍历字符串
>
> String str="abc";
>
> *方法一*
>
> >  for (int i=0;i<arr.length;i++){	
>
> > ​	sout(str.charAt(i));
>
> > //sout(str.subString(i,i+1);
>
> > }
>
> *方法二*
>
> > char [] arr = str.toCharArray();
> >
> > for (int i =0;i<arr.length();i++){	
> >
> > ​	sout(arr[i])
> >
> > }
>
> 那么go 语言中有哪些遍历字符串的方法呢



<kbd> code</kbd>

###  2. golang 的遍历

#### 2.1 方式一

> 这种方式是类似java 的一种方式，下面看代码

```
str:="abc"
for i:=0;i<len(str);i++{
	fmt.Printlf("%c",str[i])
}
//ps len(str) ==3
// output: a,b,c
```

> *但是如果存在中文*
>
> str:="我abc"
>
> len(str) ==6 // go 中中文是 utf-8 编码的，在内存种占据3个字节
>
> 遍历出来的数据也包含乱码，

#### 2.2 方式二

> 第二种方式极具go 特色，凡是涉及到遍历的（数组，字典，字符，切片） 都可以用

```go
str="我abc"
for _,v:=range str{
	fmt.Println("%c",v)
}
out: 我，a,b,c
```



#### 2.3 方式三

> 第一种方式的改良，和java 很类似
>
> 先看代码

```go
str="我abc"
rn:=[]rune(str)
fmt.Println(len(str))
for i:=0;i<len(rn);i++{
	fmt.Printf("%c",rn[i])
}
out: len:4
 我，a,b,c
```



#### 3.总结

>  为何方式三就可以打印出预期的长度4，完整的中文呢
>
> 1.先来说下 
>
> ```
> type byte = uint8
> 
> // rune is an alias for int32 and is equivalent to int32 in all ways. It is
> // used, by convention, to distinguish character values from integer values.
> type rune = int32
> ```
>
> byte是uint8的别名，两者完全等价。定义byte，只是因为按照惯例，使对字节值和8位无符号整数值进行区分
>
> rune是int32的别名，两者完全等价 只是因为按照惯例，将字符值与整数值进行区分
>
> 2. 至于golang 的源码，我还不得而知，但是java String 内部也维护了字节数组，在展示的时候，按照unicode 编码 2个字节 合二为一 转换成 char 展示
>
>    ，如第一种方式估计也是直接遍历字节，没有处理
>
>    第三种 是将3个（或者4,因为rune 是int32，具体我就不太清楚了）字节，作为一个字符来展示，所以可以正确显示汉字（utf-8 编码 占据三个字节）
>
>    

