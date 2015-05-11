## 1 Web及网络基础
- HTTP的历史
1 3项WWW构建技术
	HTML //超文本标记语言
	HTTP //超文吧传输协议
	URI //统一资源定位符
2 早期浏览器 Mosaic 
HTTP/1.0 http://www.ietf.org/rfc/rfc1945.txt
HTTP/1.1 http://www.ietf.org/rfc/rfc2616.txt
HTTP/2
3 TCP/IP
分层
	应用层 //向用户提供应用服务时通信的活动
		FTP //文件传输协议
		DNS //域名系统 提供域名到IP地址之间的解析服务
		HTTP
	传输层 //提供处于网络连接中两台计算机之间的数据传输
		TCP //传输控制协议 三次握手 发送端发送一个带有SYN标志的数据包给对方 接受端收到后 回传一个带有SYN/ACK标志的数据包
		以示传达确认信息 最后 发送端再回传一个带ACK标志的数据包 代表握手结束
		UDP //用户数据报协议
	网络层 //处理网络上流动的数据包(网络传输的最小数据单位) 该层规定了通过怎样的路径到达对方计算机 并把数据包传给对方
		IP //把数据包传给对方 IP地址(节点被分配到的地址) MAC地址(网卡所属的固定地址)
		ARP //根据通信方的IP地址反查出对应的MAC地址
	链路层(数据链路层 网络接口层) //处理连接网络的硬件部分
4 URI 统一资源标识符 //RFC2396
	Uniform //规定统一的格式处理多种不同类型的资源
	Resource //可标识的任何东西
	Identifier //可标识的对象
URL 统一资源定位符
格式 http://user:pass@www.example.jp:80/dir/index.htm?uid=1#ch1
	协议方案名 http://
	登录信息 user:pass (可选)
	服务器地址 www.example.jp
	服务器端口号 80
	带层次的文件路径 dir/index.htm
	查询字符串 uid=1
	片段标识符 ch1