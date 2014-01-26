KeyDiary API Documents
=============

第一版暂时采用 [HTTP BASIC AUTH](http://zh.wikipedia.org/zh-cn/HTTP%E5%9F%BA%E6%9C%AC%E8%AE%A4%E8%AF%81) 验证方式。

每次请求都请带上 `source` 和 `accessKey` 两个参数，否则会返回 `{stat:5}` 错误。

## 用户

### 验证用户

验证指定用户

##### URL

[http://api.keydiary.net/accounts/verify](http://api.keydiary.net/accounts/verify)

##### HTTP 请求方式

GET

##### 请求参数

无

##### 返回结果

```json
{
"stat":1,
"data":{"uid":1,"email":"rockdai@qq.com","username":"rockdai","created":"2013-02-26 20:10:59"}
}
```

- - -

## 日记

### 获取所有日记

获取当前用户的所有日记

##### URL

[http://api.keydiary.net/diaries](http://api.keydiary.net/diaries)

##### HTTP 请求方式

GET

##### 请求参数

无

##### 返回结果

```json
{
"stat":1,
"data":{
  "diaries": [
    {
      "did": "445",
      "d": "2013-03-05",
      "content": "mock data",
      "created": "2013-03-09 23:22:03",
      // 地理位置
      "geolocation": {
        // 纬度值, 格式: 小数点后保留六位
        "lat": 16.324512,
        // 经度值, 格式: 小数点后保留六位
        "lon": 16.312341,
        // 国家
        "country": "中国",
        // 省份
        "province": "浙江省",
        // 城市
        "city": "杭州市",
        // 区县
        "district": "西湖区",
        // 乡镇
        "town": "古荡镇",
        // 村庄(社区)
        "village": "益乐社区",
        // 主路
        "main_street": "益乐路",
        // 支路
        "sub_street": "",
        // 标志性POI
        "poi": "世纪新城东区西门"
      }
    },
    ...
  ],
  "startDate": 1285862400000,
  "startDateFormat": "2010-10-01",
  "endDate": 1364140799999,
  "endDateFormat": "2013-03-24"
 }
}
```

其中 `startDate` 是`用户注册的时间`和`用户第一篇日记的时间`中，较早的一个；`endDate` 是服务器返回的当前时间。


### 获取指定日期范围的日记

获取当前用户指定日期范围的日记

##### URL

http://api.keydiary.net/diaries/:from(YYYY-MM-DD)/:to(YYYY-MM-DD)

##### HTTP 请求方式

GET

##### 请求参数

无

##### 返回结果

```json
{
"stat":1,
"data":{
  "diaries": [
    {
      "did": "445",
      "d": "2013-03-05",
      "content": "mock data",
      "created": "2013-03-09 23:22:03",
      // 地理位置
      "geolocation": {
        // 纬度值, 格式: 小数点后保留六位
        "lat": 16.324512,
        // 经度值, 格式: 小数点后保留六位
        "lon": 16.312341,
        // 国家
        "country": "中国",
        // 省份
        "province": "浙江省",
        // 城市
        "city": "杭州市",
        // 区县
        "district": "西湖区",
        // 乡镇
        "town": "古荡镇",
        // 村庄(社区)
        "village": "益乐社区",
        // 主路
        "main_street": "益乐路",
        // 支路
        "sub_street": "",
        // 标志性POI
        "poi": "世纪新城东区西门"
      }
    },
    ...
  ]
 }
}
```

### 获取指定日期的日记

获取当前用户指定日期的日记

##### URL

http://api.keydiary.net/diaries/:date(YYYY-MM-DD)

##### HTTP 请求方式

GET

##### 请求参数

无

##### 返回结果

```json
{
  "stat":1,
  "data": {
    "did": "445",
    "d": "2013-03-05",
    "content": "mock data",
    "created": "2013-03-09 23:22:03",
    // 地理位置
    "geolocation": {
      // 纬度值, 格式: 小数点后保留六位
      "lat": 16.324512,
      // 经度值, 格式: 小数点后保留六位
      "lon": 16.312341,
      // 国家
      "country": "中国",
      // 省份
      "province": "浙江省",
      // 城市
      "city": "杭州市",
      // 区县
      "district": "西湖区",
      // 乡镇
      "town": "古荡镇",
      // 村庄(社区)
      "village": "益乐社区",
      // 主路
      "main_street": "益乐路",
      // 支路
      "sub_street": "",
      // 标志性POI
      "poi": "世纪新城东区西门"
    }
  }
}
```


### 发表日记

发表新日记

##### URL

[http://api.keydiary.net/diaries/create](http://api.keydiary.net/diaries/create)

##### HTTP 请求方式

POST

##### 请求参数

Required

* d 日记日期，格式为 YYYY-MM-DD
* content 日记内容，长度不能超过 14 个字符

Optional

* lat 纬度值, 格式: 小数点后保留六位
* lon 经度值, 格式: 小数点后保留六位
* country 国家
* province 省份
* city 城市
* district 区县
* town 乡镇
* village 村庄(社区)
* main_street 主路
* sub_street 支路
* poi 标志性 POI

##### 返回结果

```json
{
"stat":1,
"data":{"d":"2013-03-13","content":"mock data","sid":2, "geolocation": {}}
}
```

### 覆盖日记

如果已存在则更新现有，否则新增一条日记

##### URL

[http://api.keydiary.net/diaries/upsert](http://api.keydiary.net/diaries/upsert)

##### HTTP 请求方式

POST

##### 请求参数

Required

* d 日记日期，格式为 YYYY-MM-DD
* content 日记内容，长度不能超过 14 个字符

Optional

* lat 纬度值, 格式: 小数点后保留六位
* lon 经度值, 格式: 小数点后保留六位
* country 国家
* province 省份
* city 城市
* district 区县
* town 乡镇
* village 村庄(社区)
* main_street 主路
* sub_street 支路
* poi 标志性 POI

##### 返回结果

```json
{
"stat":1,
"data":{"d":"2013-03-13","content":"mock data","sid":2, "geolocation": {}}
}
```

### 更新日记

更新指定日期的日记

##### URL

[http://api.keydiary.net/diaries/update](http://api.keydiary.net/diaries/update)

##### HTTP 请求方式

POST

##### 请求参数

Required

* d 日记日期，格式为 YYYY-MM-DD
* content 日记内容，长度不能超过 14 个字符

Optional

* lat 纬度值, 格式: 小数点后保留六位
* lon 经度值, 格式: 小数点后保留六位
* country 国家
* province 省份
* city 城市
* district 区县
* town 乡镇
* village 村庄(社区)
* main_street 主路
* sub_street 支路
* poi 标志性 POI

##### 返回结果

```json
{"stat":1}
```

### 追加日记   

在指定日期的日志后面追加日志，总长度仍然有7个的限制

##### URL

[http://api.keydiary.net/diaries/append](http://api.keydiary.net/diaries/append)

##### HTTP 请求方式  

POST

##### 请求参数

Requried

* d 日记日期，格式为 YYYY-MM-DD
* content 日记内容，长度不能超过 14 个字符

Optional

* lat 纬度值, 格式: 小数点后保留六位
* lon 经度值, 格式: 小数点后保留六位
* country 国家
* province 省份
* city 城市
* district 区县
* town 乡镇
* village 村庄(社区)
* main_street 主路
* sub_street 支路
* poi 标志性 POI

##### 返回结果

```json
{
"stat":1,
"data":{"d":"2013-03-13","content":"mock data","sid":2, "geolocation": {}}
}
```


### 删除日记

删除指定日期的日记

##### URL

[http://api.keydiary.net/diaries/remove](http://api.keydiary.net/diaries/remove)

##### HTTP 请求方式

POST

##### 请求参数

* d 日记日期，格式为 YYYY-MM-DD

##### 返回结果

```json
{"stat":1}
```

- - -

## 建议反馈

### 添加一条反馈

##### URL

[http://api.keydiary.net/feedback](http://api.keydiary.net/feedback)

##### HTTP 请求方式

POST

##### 请求参数

* content 反馈的内容

##### 返回结果

```json
{
"stat":1,
"data":{
  "content": "mock data",
  "sid": 2
 }
}
```
