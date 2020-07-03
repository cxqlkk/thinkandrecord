GET /source/log/_search
{
  "query": {
    "match_all": {}
  },
  "sort": {
    "create_time": {
      "order": "desc"
    }
  }
}


报错：Fielddata is disabled on text fields by default. Set fielddata=true


备注日期格式：2006/01/02 15:04:05
（elastic.co/guide/en/elasticsearch/reference/current/date.html）

修改
```
PUT source/_mapping/log/
{
    "properties":{
        "create_time":{
            "type":"text",
            "fielddata":true
        }
    }
}
```