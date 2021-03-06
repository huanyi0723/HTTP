## 6 HTTP首部
1 HTTP报文
	报文首部 //在客户端和服务端处理时起至关重要的作用的信息几乎都在里面
	空行 //CR + LF
	报文主体 //所需要的用户和资源的信息都在里面

HTTP请求报文
	报文首部 //请求行（方法 URI HTTP版本） 首部字段（请求 通用 实体） 其他
	空行 //CR + LF
	报文主体

HTTP响应报文
	报文首部 //状态行（HTTP版本 状态吗即数字和原因短语） 首部字段（响应 通用 实体） 其他
	空行 //CR + LF
	报文主体

2 HTTP首部字段
作用 
	给浏览器和服务器提供报文主体大小 所使用的语言 认证信息等
字段结构
	首部字段名：字段值
	例如
		Content-Type：text/html
		Keep-Alive：timeout=15，max=100
4种HTTP首部字段类型 //HTTP/1.1规范定义了47种首部字段 RFC2626
	通用首部字段 //请求报文和响应报文两方都会使用的首部
		Cache-Control //控制缓存的行为
		例子 
			Cache-Control: private, max-age=0, no-cache
			缓存请求指令
				no-cache //强制向源服务器再次验证
				no-store //不缓存请求或响应的任何内容 暗示请求或响应中包含机密信息
				max-age= //响应的最大Age值 判定缓存资源的缓冲时间数值比指定的更小 就接受缓存的资源
				max-stale = //接收已过期的响应
				min-fresh= //期望在指定时间内的响应仍有效 指定 min-fresh为60秒 过了60秒的资源都无法作为响应返回了
				no-transform //代理不可更改媒体类型
				only-if-cached //从缓存获取资源 要求缓存服务器不重新加载响应 也不会再次确认资源有效性
				cache-extension //新指令标记
			缓存响应指令
				public //可向任意方提供响应的缓冲
				private //仅向特定用户返回响应
				no-cache //缓存前必须先确认有效性
				no-store //不缓存请求或响应的任何内容 暗示请求或响应中包含机密信息
				no-transform //代理不可更改媒体类型 可防止缓存或代理压缩图片等类似操作
				must-revalidate //可缓存但必须向源服务器进行确认 代理会向源服务器再次验证即将返回的响应缓存目前是否仍然有效
				proxy-revalidate //要求中间缓存服务器对缓存的响应有效性再进行确认
				max-age= //响应的最大Age值 资源保存为缓存的最长时间
				s-maxage= //公共缓存服务器响应的最大Age值
				cache-extension //新指令标记 仅对理解它的缓存服务器有意义
		Connection //逐条首部、连接的管理
			作用
				1 控制不再转发给代理的首部字段
					Connection: 不再转发的首部字段名
				2 管理持久连接
					Connection:Keep-Alive //持久连接
					Connection:close //断开连接		
		Data //创建报文的日期时间
			Data: Tue, 03 Jul 2012 04:40:59 GMT
		Pragma //报文指令 历史遗留字段 向后兼容
			Pragma: no-cache //只能用在客户端发送请求中 客户端会要求所有中间服务器不返回缓存的资源
		Trailer //报文末端的首部一览 事先说明报文主体后记录了哪些首部字段
		Transfer-Encoding //指定报文主体的传输编码方式 仅对分块传输编码有效
			Transfer-Encoding: chunked
		Upgrade //升级为其他协议 检测HTTP协议以及其他协议是否可使用更高的版本进行通信
		Via //代理服务器的相关信息 追踪客户端与服务器之间的请求和响应报文的传输路径
		Warning //错误通知 与缓存相关的问题的警告
			110 //响应已过期
			111 //再验证失败
			112 //断开连接操作
			113 //试探性过期
			199 //杂项警告
			214 //使用了转换
			299 //持久杂项警告
	请求首部字段 //补充了请求的附加内容 客户端信息 响应内容相关优先级等信息
		Accept //用户代理可处理的媒体类型及媒体类型的相对优先级
			Accept:text/html, application/xhtml+xml, application/xml; q=0.9,*/*; q=0.8
			文本文件 text/html text/plain text/css application/xhtml+xml application/xml
			图片文件 image/jpeg image/gif image/png
			视频文件 video/mpeg video/quicktime
			应该程序使用的二进制文件 application/octet-stream application/zip
		Accept-Charset //优先的字符集
			Accept-Charset: iso-8859-5, unicode-1-1; q=0.8
		Accept-Encoding //优先的内容编码
			gzip
			compress
			deflate
			identity
		Accept-Language //优先的语言
			Accept-Language: zh-cn,zh; q=0.7,en-us; q=0.3
		Authorization //Web认证信息 RFC2616
		Expect //期待服务器的特点行为
		From //用户的电子邮箱地址
		Host //请求资源所在的服务器
			告知服务器请求的资源所处的互联网主机名和端口号
		//条件请求 只有指定条件为真时才会执行请求
		If-Match //比较实体标记
			If-Match: "123456" //告知服务匹配资源所用的实体标记(ETag)值 服务器会对比两个值 当相同时才执行请求 否则返回412 Precondition Failed
		If-Modified-Since //比较资源的更新时间
			如果该值早于资源的更新时间 则处理该请求 否则 返回304 Not Modified
		If-None-Match //比较实体标记 与If-Match 相反
			该实体标记(ETag)值与请求资源的ETag不一致时 告知服务器处理该请求
		If-Range //资源未更新时发送实体Byte的范围请求
			一致时作为范围请求处理 反之返回全体资源
		If-Unmodified-Since //比较资源的更新时间 与If-Modified-Since相反
			指定的请求资源只有在字段值内指定的日期时间之后 未发生更新的情况下 才能处理请求
		Max-Forwards //最大传输逐跳数
			指定可经过的服务器的最大数目
		Proxy-Authorization //代理服务器要求客户端的认证信息
		Range //实体的字节范围请求
		Referer //对请求中URI的原始获取方
		TE //传输编码的优先级
		User-Agent //HTTP客户端程序的信息
			创建请求的浏览器和用户代理名称等信息传给服务器
	响应首部字段 //补充了相应的附加内容 也会要求客户端附加额外的内容信息
		Accept-Ranges //是否接受字节范围请求
			告知客户端服务器是否能处理范围请求以指定获取服务器某个部分的资源
			可处理为bytes 反之为none
		Age //推算资源创建经过时间
			告知客户端源服务器在多久之前创建了响应
		ETag //资源的匹配信息
			告知客户端实体标识 可将资源以字符串形式做唯一性标识的方式
		Location //令客户端重定向至指定URI
			将响应接受方引导至某个与请求URI位置不同的资源
		Proxy-Authenticate //代理服务器对客户端的认证信息
			Proxy-Authenticate: Basic realm="Usagidesign Auth" //把由代理服务器所要求的认证信息发送给客户端
		Retry-After //对再次发起请求的时机要求
			告知客户端应该在多久之后再次发送请求
		Server //HTTP服务器的安装信息
			Server:Apache/2.2.17(Unix) //告知客户端当前服务器上安装的HTTP服务器应用程序的信息 包括版本号和安装时启用的可选项
		Vary //代理服务器对缓存的管理信息
		WWW-Authenticate //服务器对客户端的认证信息
			告知客户端适用于访问请求URI所指定资源的认证方案和带参数提升的资询
	实体首部字段 //补充了资源内容更新时间等与实体有关的信息
		Allow //资源可支持的HTTP方法
			通知客户端能够支持Request-URI指定资源的所有HTTP方法
			当服务器接收到不支持的HTTP方法时 会以状态码405 Method Not Allowed
		Content-Encoding //实体主体适用的编码方式
			gzip
			compress
			deflate
			identity
		Content-Language //实体主体的自然语言
			Content-Language: zh-CN
		Content-Length //实体主体的大小
		Content-Location //替代对应资源的URI
			给出报文主体相对应的URI
		Content-MD5 //实体主体的报文摘要
			检查报文主体在传输过程中是否保持完整 以及确认传输到达
		Content-Range //实体主体的位置范围
			Content-Range: bytes 5001-10000/10000
		Content-Type //实体主体的媒体类型
			Content-Type: text/html; charset=UTF-8
		Expires //实体主体过期的日期时间
			将资源失效的日期告知客户端
		Last-Modified //资源的最后修改日期时间
非HTTP/1.1 首部字段	RFC4229
	Cookie //工作机制是用户识别和状态管理
	与Cookie有关的首部字段
		Cookie //请求首部字段 服务器接收到的Cookie信息
			Cookie: status=enable
		Set-Cookie //响应首部字段 开始状态管理所使用的Cookie信息
			NAME=VALUE //赋予Cookie的名称和其值
			expires=DATA //Cookie的有效期
			path=PATH //将服务器上的文件目录作为Cookie的适用对象
			domain=域名 //作为Cookie适用对象的域名
			Secure //仅在HTTPS安全通信时才会发送Cookie
			HttpOnly //加以限制 使Cookie不能被JavaScript脚本访问
				防止跨站脚本攻击对Cookie的信息窃取

其它非标准首部字段
	X-Frame-Options //响应首部 控制网站内容在其他Web网站的Frame标签内的显示问题 防止点击劫持
		DENY //拒绝
		SAMEORIGIN //仅同源域名下的页面匹配时许可
	X-XSS-Protection //控制浏览器XSS防护机制的开关
		0 // 将XSS过滤设置成无效状态
		1 // 有效状态
	DNT //请求首部 拒绝个人信息被收集
		0 //同意被追踪
		1 //拒绝
	P3P //在线隐私偏好技术
首部的分类
		端到端首部 //会转发给请求/响应对应的最终接受目标 并且必须保存在由缓存生成的响应中 规定它必须被转发
		逐跳首部 //只对单次转发有效 会通过缓存或代理而不再转发 共8个
			Connection
			Keep-Alive
			Proxy-Authenticate
			Proxy-Authorization
			Trailer
			TE
			Transfer-Encoding
			Upgrade

