## 2 简单HTTP协议
1 客户端 //请求访问文本和图像等资源的一端
服务端 //提供资源响应的一端
2 具体示例
请求报文构成
请求方法 请求URI 协议版本
可选的请求首部字段
内容实体

例如
POST /form/entry HTTP/1.1

Host: hackr.jp
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 16

name=ueno&age=37


响应报文的构成
协议版本 状态码 状态码的原因短语
可选的响应首部字段
实体主体

例如
HTTP/1.1 200 OK
Data: Tue. 10 Jul 2012 06:50:15 GMT
Content-Length: 362
Content-Type: text/html

<html>

3
HTTP是不保存状态协议 //Cookie

4 指定请求URI的方式
URI为完整的请求URI
	GET http://hackr.jp/index.htm HTTP/1.1
在首部字段HOST中写明网络域名或IP地址
	GET /index.htm HTTP/1.1
	Host: hackr.jp
查询HTTP服务器支持HTTP方法种类
	OPTIONS * HTTP/1.1

5 HTTP/1.1可使用的方法
GET 获取资源
	请求
		GET /index.html HTTP/1.1
		Host: www.hackr.jp
	响应
		返回index.html的页面资源
	请求
		GET /index.html HTTP/1.1
		Host: www.hackr.jp
		If-Modified-Since: Thu, 12 Jul 2012 07:30:00 GMT
	响应
		返回2012年7月12日7点30分以后更新过的index.html页面资源
		未更新 以状态码304 Not Modified作为响应返回

POST 传输实体主体 虽然GET方法也可传输实体的主体 但一般不用GET方法进行传输
	请求
		POST /submit.cgi HTTP/1.1
		Host: www.hackr.jp
		Content-Length:1560
	响应
		返回submit.cgi接受数据的处理结果

PUT 传输文件 由于PUT方法自身不带验证机制 一般不用改方法 采用REST的Web网站可能开发该方法
	请求
		PUT /example.html HTTP/1.1
		Host: www.hackr.jp
		Content-Type:text/html
		Content-Length:1560
	响应
		响应返回状态码204 No Content //该html已存在服务器上

HEAD 获得报文首部 和GET方法一样 只是不返回报文主体部分 用于确认URI的有效性和资源的更新日期
	请求
		HEAD /index.html HTTP/1.1
		Host: www.hackr.jp
	响应
		返回index.html有关的响应首部

DELETE 删除文件 与PUT相反 由于DELETE方法自身不带验证机制 一般不用改方法 采用REST的Web网站可能开发该方法
	请求
		DELETE /example.html HTTP/1.1
		HOST: www.hackr.jp
	响应
		响应返回状态码204 No Content //该html已从该服务器上删除

OPTIONS 询问支持的方法
	请求
		OPTIONS * HTTP/1.1
		Host: www.hackr.jp
	响应
		HTTP/1.1 200 OK
		Allow:GET,POST,HEAD,OPTIONS

TRACE 追踪路径 让服务端将之前的请求通信环回给客户端 不常用 容易引发跨站追踪攻击
	请求
		TRACE HTTP/1.1
		Host: hackr.jp
		Max-Forwards:2
	响应
		HTTP/1.1 200 OK
		Content-Type: message/http
		Content-Length: 1024

		TRACE HTTP/1.1
		Host: hackr.jp
		Max-Forwards:2


CONNECRT 要求用隧道协议连接代理
	要求在代理服务器通信时建立隧道 实现用隧道协议进行TCP通信
	主要使用SSL和TLS协议把通信内容加密后经网络隧道传输

	请求
		CONNECRT proxy.hackr.jp:8080 HTTP/1.1
		Host: proxy.hackr.jp
	响应
		HTTP/1.1 200 OK //之后进入网络隧道

6 HTTP/1.0和HTTP/1.1支持的方法
HTTP/1.0 LINK UNLINK GET POST PUT HEAD DELETE
HTTP/1.1 GET POST PUT HEAD DELETE OPTIONS TRACE CONNECRT

7 持久连接
管线化

8 Cookie
Set-Cookie首部字段信息
	请求报文 //没有Cookie信息的状态
		GET /reader HTTP/1.1
		Host: hackr.jp
	响应报文 //服务端生成Cookie信息
		HTTP/1.1 200 OK
		Data: Thu, 12 Jul 2012 07:12:20 GMT
		Server: Apache
		<Set-Cookie: sid=1342077140226724; path=/; expires=Wed,10-Oct-12 07:12:20 GMT>
	请求报文 //自动发送保存的Cookie信息
		GET /image/ HTTP/1.1
		Host: hackr.jp
		Cookie: sid=1342077140226724