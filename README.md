KeyDiary API doc
=============

第一版暂时采用 [HTTP BASIC AUTH](http://zh.wikipedia.org/zh-cn/HTTP%E5%9F%BA%E6%9C%AC%E8%AE%A4%E8%AF%81) 验证方式。

每次请求都请带上 `source` 和 `accessKey` 两个参数，否则会返回 `{stat:5}` 错误。

## 用户

#### 验证用户

验证指定用户

###### URL

[http://api.keydiary.net/accounts/verify](http://api.keydiary.net/accounts/verify)

###### HTTP 请求方式

GET

###### 请求参数

无

###### 返回结果

```json
{
"stat":1,
"data":{"uid":1,"email":"rockdai@qq.com","username":"rockdai","created":"2013-02-26 20:10:59"}
}
```

## 日记

#### 获取日记

获取当前用户的所有日记

###### URL

[http://api.keydiary.net/diaries](http://api.keydiary.net/diaries)

###### HTTP 请求方式

GET

###### 请求参数

无

###### 返回结果

```json
{
"stat":1,
"data":{
  "diaries": [{"did":"445","d":"2013-03-05","content":"mock data"},{"did":"446","d":"2013-03-12","content":"mock data"}],
  "startDate": 1358956800000,
	"endDate": 1363622399999
}
}
```

其中 `startDate` 是`用户注册的时间`和`用户第一篇日记的时间`中，较早的一个；`endDate` 是服务器返回的当前时间。

#### 发表日记

发表新日记

###### URL

[http://api.keydiary.net/diaries/create](http://api.keydiary.net/diaries/create)

###### HTTP 请求方式

POST

###### 请求参数

* d 日记日期，格式为 YYYY-MM-DD
* content 日记内容，长度不能超过 14 个字符

###### 返回结果

```json
{
"stat":1,
"data":{"d":"2013-03-13","content":"mock data","source":2}
}
```

#### 更新日记

更新指定日期的日记

###### URL

[http://api.keydiary.net/diaries/update](http://api.keydiary.net/diaries/update)

###### HTTP 请求方式

POST

###### 请求参数

* d 日记日期，格式为 YYYY-MM-DD
* content 日记内容，长度不能超过 14 个字符

###### 返回结果

```json
{"stat":1}
```

#### 删除日记

删除指定日期的日记

###### URL

[http://api.keydiary.net/diaries/remove](http://api.keydiary.net/diaries/remove)

###### HTTP 请求方式

POST

###### 请求参数

* d 日记日期，格式为 YYYY-MM-DD

###### 返回结果

```json
{"stat":1}
```
