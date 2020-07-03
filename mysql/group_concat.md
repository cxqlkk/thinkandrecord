|x |x |x |
|--|--|--|
|A|xx|b|
|A|cc|b|
|B|xx|c


`主从表是1对多的情况，如果想查询从表的的时候，需要主表的部分数据`
`为了避免展示多条数据，需要多条数据合并，那么就可以用GROUP_CONCAT(distinct people.MOBILE_PHONE_NUM SEPARATOR " " )`


distinct 可以去重
SEPARATOR 可以指定分隔符
还可以排序