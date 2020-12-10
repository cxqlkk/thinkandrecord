### UTC 和 CST 时间

UTC 是  零时区时间
    世界协调时间（UTC）是世界上不同国家用来调节时钟和时间的主要时间标准。

CST 是 中央标准时间

 Central Standard Time (USA) UT-6:00（美国cst时间：零区时减6个小时）

            Central Standard Time (Australia) UT+9:30（澳大利亚cst：加9个半小时）

            China Standard Time UT+8:00（中国cst:加8个小时）

            Cuba Standard Time UT-4:00  （古巴cst:减4个小时）             

如：当UTC时间为0点时，中国CST时间为8点，因为零时区和中国北京时区相差8个时区。

time.Parse(layout,"2020-09-07 15:22:11")
得到的是 UTC 时间  

time.ParseLocation(layout,"2020-09-07 15:22:11",time.local)
得到是 CST 时间

### 注意了，如果数据库字段是 dataTime
程序 字段类型 是时间格式  如果 数据库连接设置了 loc=Local
那么  go mysql 将会对时间转换 为 CST 时间
如果 字段的时间格式 是UTC 时间，那么 就会转换为 CST 时间 +8，造成了结果加8
### ps :程序时间格式 必须是 CST ，并且 loc =local 才是正确的

如果不设置 loc=local 那么 如果是 cst 就会 -8 


### import 也就是说， 程序里的字段时间类型和 数据库 loc 一致 ，结果才会正确 （但是最好是用 CST 时间）