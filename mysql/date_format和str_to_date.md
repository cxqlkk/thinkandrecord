STR_TO_DATE ("字符"，格式)-》 日期
DATE_FORMAT（时间，格式） 字符

> 实践发现DATE_FORMAT（时间，格式） 时间 也可以是字符串
> 也就是上述两者在格式上基本相同
> 但是有些注意点
> 函数的参数（日期） 必须 包含年月日，否则 不管什么格式 都转为null
>STR_TO_DATE 格式 必须包含 %Y-%m-%d 否则也是null


*ps :感觉DATE_FORMAT更有效（可以转换为各种格式，毕竟是字符串）*

select STR_TO_DATE("2020-05-01","%Y-%m") null
select STR_TO_DATE("2020-05-01","%Y-%m-%d") 2020-05-01
select STR_TO_DATE("2020-05","%Y-%m-%d") null
select STR_TO_DATE("2020-05-01 15","%Y-%m-%d") 2020-05-01
select STR_TO_DATE("2020-05-01 15","%Y-%m-%d %H") 2020-05-01 15:00:00
select DATE_FORMAT("2020-05-01","%Y-%m") 2020
select DATE_FORMAT("2020-05","%Y-%m") null