## 4 HTTP状态码
1 状态码 当客户端向服务端发送请求时 描述返回的请求结果
	由3位数字和原因短语组成
状态码类别
	1** 信息性状态码 接受的请求正在处理
	2** 成功状态码 请求正常处理完毕
	3** 重定向状态码 需要进行附加操作以完成请求
	4** 客户端错误状态码 服务端无法处理请求
	5** 服务器错误状态码 服务器处理请求出错
状态码个数
	RFC2616 40种
	RFC4918、5842和RFC6585 60种
	常用 14种

2 2** 成功
	200 OK //客户端发送的请求在服务端被正常处理了
	204 No Content //请求已成功处理 但返回的响应报文不含实体的主体部分
	206 Partial Content //客户端进行了范围请求 服务端执行了这部分的GET请求
3 3** //浏览器需要执行某些特殊的处理以正确处理请求
	301 Moved Permanently //永久性重定向 请求的资源已经分配新的URI 以后应使用资源现在所指的URI
	302 Found //临时性重定向 请求的资源已经分配新的URI 希望用户使用新的URI访问
	303 See Other //请求的资源存在另一个URI 应使用GET方法定向获取指定的资源
	304 Not Modified //客户端发送附带条件的请求时 服务端允许请求访问资源 但未满足条件的情况
	307 Temporary Redirect //临时性重定向
4 4** //客户端错误
	400 Bad Request //请求报文中存在语法错误
	401 Unauthorized //发送的请求需要通过HTTP认证 若之前已进行过一次请求 则用户认证失败
	403 Forbidden //请求资源的访问被服务器拒绝了
	404 Not Found //服务器上无法找到请求的资源
5 5** //服务器错误
	500 Internal Server Error //服务端执行请求时发生了错误
	503 Service Unavailable //服务器暂时处于超负荷或正在进行停机维护
