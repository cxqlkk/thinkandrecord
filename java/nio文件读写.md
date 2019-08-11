## <center>NIO-初探之文件读写</center>

### 1 前言

> 其实先前按照其他人的博客，写过nio的文件读写，但都忘了，现在重新学习一下

### 2 知识点概述

> 类：buffer,channel
>
> 方法：allocateDirect(),allocate(),flip(),clear()
>
> 字段：position ,limit ,capacity
>
> 说明： 本文只是粗浅的使用，涉及的只是基本的知识

### 3 文件读写示例

##### 3.1 示例一

```java
String readFilePath="/home/cxq/java_int.txt";
String writeFilePath="/home/cxq/java_out.txt";
Channel readChannel = new FileInputStream(new File(readFilePath)).getChannel();
ByteBuffer buffer = ByteBuffer.allocate(1024);
//allocateDirect(),直接操作物理内存，据说读写效率更高，但销毁内存代价稍大
[] [] [] [] [] [] [] [] [] [] [];
 position   			 limit|capacity
 //position, 下一次读/或者写的位置
 //limit 读或者写的最大位置（此处都是指索引）
 //capacity buffer 的容量，*固定不变*
 //一、初始化的时候， position=0,limit=capacity=len(buffer)(此处指代buffer最大容量)
 readChannel.read(buffer);
//二、假如 本次读取了 N<1024 字节
//position=N,limit=capacity
buffer.flip();//读状态转换为写状态
//三、 limit=position,position=0
Channel writeChannel = new FileOutputStream(new File(writeFilePath)).getChannel();
writeChannel.write(buff);
//四，position=limit
buffer.clear();
//五，position=0, limit=capacity //重置

    
```

```java
 FileInputStream inputStream = new FileInputStream(newFile(readFilePath));
 Channel readChannel = inputStream.getChannel();
 ByteBuffer buffer = ByteBuffer.allocate(10);
 FileOutputStream outputStream = new FileOutputStream(new File(writeFilePath),true);
  int len =-1;
 while((len=((FileChannel) readChannel).read(buffer))!=-1){
            buffer.flip();
            Channel writeChannel = outputStream.getChannel();
            ((FileChannel) writeChannel).write(buffer);
            buffer.clear();
  }
        //ByteBuffer.allocateDirect();
```

