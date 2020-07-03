
[
    {
        "正常":11
    },
    {
        "错误":22
    }
]

```
GET /source/log/_search
{
  "size": 0,
  "aggs": {
    "group_b": { (结果数据名)
      "terms": {
        "field": "status"  （分组字段）
      }
    }
  }
}
```

### 结果 分词了。。。

```

{
 
  "aggregations": {
    "group_b": {
      "doc_count_error_upper_bound": 0,
      "sum_other_doc_count": 0,
      "buckets": [
        {
          "key": "常",
          "doc_count": 19
        },
        {
          "key": "正",
          "doc_count": 19
        },
        {
          "key": "出",
          "doc_count": 2
        },
        {
          "key": "错",
          "doc_count": 2
        }
      ]
    }
  }
}
```


## 解决

```
POST /source/_mapping/log
{
  "properties": {
        "status": {(stauts 为字段名)
            "type": "text",
            "fielddata": true,
            "fields": {"raw": {"type": "keyword"}}
            }
        }
}

```


```
GET /source/log/_search
{
  "size": 0,
  "aggs": {
    "group_b": { (结果数据名)
      "terms": {
        "field": "status.keyword"  （分组字段）
      }
    }
  }
}
```
