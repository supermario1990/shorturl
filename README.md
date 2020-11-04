# shorturl

go_zero [pull/157](https://github.com/tal-tech/go-zero/pull/157) 示例

一：正常情况

1. 进入api目录，启动rest server: `go run shorturl.go`

2.  访问服务：`curl -i "http://localhost:8888/shorten?url=http://www.xiaoheiban.cn"`

   5s后会响应：

   ```http
   HTTP/1.1 200 OK
   Content-Type: application/json
   Date: Wed, 04 Nov 2020 08:19:57 GMT
   Content-Length: 14
   
   {"shorten":""}
   ```

二：模拟优雅关闭场景

1. 进入api目录，启动rest server: `go run shorturl.go`
2. 访问服务：`curl -i "http://localhost:8888/shorten?url=http://www.xiaoheiban.cn"`，等5s才会响应
3. 迅速在另一个终端使用 `kill -15 pid` 优雅关闭rest server（这步动作快点）
4.  http响应:

```http
curl: (52) Empty reply from server
```

三：更新为PR代码，重新验证优雅关闭场景

步骤同上，不同的是第4步http响应：

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 04 Nov 2020 08:20:06 GMT
Content-Length: 14
Connection: close

{"shorten":""}
```



