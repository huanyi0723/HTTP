## 7 HTTPS
1 HTTP的缺点
	1 通信使用明文不加密 内容有可能被窃取
		抓包工具 Wireshark
		加密处理方式
			通信的加密 SSL 安全套接层 TLS 安全传输层协议 HTTPS 与SSL组合使用的HTTPS
			内容的加密 报文主体加密处理
	2 不验证通信方的身份 因此有可能遭遇伪装
		服务器是否就是发送请求中URL真正指定的主机 返回的响应是否真的返回到实际提出请求的客户端
		解决办法 SSL 证书
	3 无法证明报文的完整性  所以有可能已遭篡改
		没有任何办法确认 发出的请求响应和接受到的请求响应是前后相同的
		中间人攻击 请求或响应在传输途中 遭攻击者拦截并篡改内容的攻击
		解决办法 MD5和SHA-1等散列值校验
2 HTTP + 加密 + 认证 + 完整性保护 = HTTPS
	加密技术
		共享密钥加密/对称密钥加密 加密和解密使用同一个密钥的方式
			存在问题 发送密钥有被窃取的风险
		公开密钥加密 使用一对非对称的密钥 私有密钥和公开密钥 发送密文的一方使用对方的公开密钥进行加密处理 对方收到被加密的信息后 再使用自己的私有密钥进行解密
			存在问题 相比共享密钥加密速度要慢
		公开密钥证书 证明公开密钥的正确性
	HTTPS的通信步骤
	