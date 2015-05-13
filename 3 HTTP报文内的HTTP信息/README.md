## 3 HTTP报文内的HTTP信息
1 HTTP报文 用于HTTP协议交互的信息 本身有多行数据构成的字符串文本
	分为报文首部和报文主体
请求报文 请求段的HTTP报文
响应报文 响应段的HTTP报文

2 请求报文首部
	请求行 //用于请求的方法 请求URI和HTTP版本
	请求首部字段 
	通用首部字段 
	实体首部字段
	其它 //可能包含HTTP的RFC里未定义的首部(Cookie)
响应报文首部
	状态行 //响应结果的状态码 原因短语和HTTP版本
	响应首部字段 
	通用首部字段 
	实体首部字段
	其它 //可能包含HTTP的RFC里未定义的首部(Cookie)

3 报文主体和实体主体的差别
报文 //HTTP通信中的基本单位 由8位组字节流组成 通过HTTP通信传输
实体 //作为请求或响应的有效载荷数据被传输 内容由实体首部和实体主体组成
	通常 报文主体等于实体主体 只有当传输中进行编码操作时 实体主体的内容发生变化 才有区别
内容编码
	gzip //GNU zip
	compress //UNIX系统的压缩标准
	deflate //zlib
	identity //不进行编码
分块传输编码 把实体主体分块的功能

4 MIME
多部分对象集合
	multipart/form-data //在web表单文件上传时使用
	multipart/byteranges

5 获取部分内容的范围请求
	Range
6 内容协商返回最合适内容
	Accept
	Accept-Charset
	Accept-Encoding
	Accept-Language
	Content-Language