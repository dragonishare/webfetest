# 附加问题
> 涉及http,性能优化等

### 1.http响应中content-type包含哪些内容
请求中的消息主体是用何种方式编码
* application/x-www-form-urlencoded
> 这是最常见的 POST 提交数据的方式 按照 key1=val1&key2=val2 的方式进行编码

* application/json
> 告诉服务端消息主体是序列化后的 JSON 字符串