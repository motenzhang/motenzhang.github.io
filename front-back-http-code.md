<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [常见状态码释义](#%E5%B8%B8%E8%A7%81%E7%8A%B6%E6%80%81%E7%A0%81%E9%87%8A%E4%B9%89)

<!-- /MarkdownTOC -->
<a id="%E5%B8%B8%E8%A7%81%E7%8A%B6%E6%80%81%E7%A0%81%E9%87%8A%E4%B9%89"></a>
## 常见状态码释义
- ~~1xx：相关信息~~(`API不需要`)
- 2xx：操作成功
- 3xx：重定向
- 4xx：客户端错误
- 5xx：服务器错误

|	HTTP 状态码 	|	原文 	|	翻译	|
| :---- | :------------ | :-------------------|
|	100	|	Continue 	|	继续	|
|	101	|	Switching Protocols 	|	切换协议	|
|	102	|	Processing 	|	处理	|
|	103	|	Early Hints 	|	早期提示	|
|	200	|	OK 	|	好	|
|	201	|	Created 	|	创建	|
|	202	|	Accepted 	|	接受	|
|	203	|	Non-Authoritative Information 	|	非权威信息	|
|	204	|	No Content 	|	无内容	|
|	205	|	Reset Content 	|	重置内容	|
|	206	|	Partial Content 	|	部分内容	|
|	207	|	Multi-Status 	|	多态	|
|	208	|	Already Reported 	|	已经报道过了	|
|	226	|	IM Used 	|	IM已使用	|
|	300	|	Multiple Choices 	|	多种选择	|
|	301	|	Moved Permanently 	|	永久移动	|
|	302	|	Found 	|	发现	|
|	303	|	See Other 	|	见其他	|
|	304	|	Not Modified 	|	没有修改	|
|	305	|	Use Proxy 	|	使用代理服务器	|
|	307	|	Temporary Redirect 	|	临时重定向	|
|	308	|	Permanent Redirect 	|	永久重定向	|
|	400	|	Bad Request 	|	错误的请求	|
|	401	|	Unauthorized 	|	不合法	|
|	402	|	Payment Required 	|	预留	|
|	403	|	Forbidden 	|	被禁止	|
|	404	|	Not Found 	|	未找到	|
|	405	|	Method Not Allowed 	|	方法不允许	|
|	406	|	Not Acceptable 	|	不能接受	|
|	407	|	Proxy Authentication Required 	|	需要代理验证	|
|	408	|	Request Timeout 	|	请求超时	|
|	409	|	Conflict 	|	冲突	|
|	410	|	Gone 	|	去了	|
|	411	|	Length Required 	|	长度要求	|
|	412	|	Precondition Failed 	|	前提条件失败	|
|	413	|	Payload Too Large 	|	有效载荷过大	|
|	414	|	URI Too Long 	|	URI太长了	|
|	415	|	Unsupported Media Type 	|	不支持的媒体类型	|
|	416	|	Range Not Satisfiable 	|	范围不满意	|
|	417	|	Expectation Failed 	|	期望失败	|
|	418	|	I’m a teapot 	|	彩蛋：我是一个茶壶	|
|	421	|	Misdirected Request 	|	错误的请求	|
|	422	|	Unprocessable Entity 	|	不可处理的实体	|
|	423	|	Locked 	|	锁定	|
|	424	|	Failed Dependency 	|	失败的依赖	|
|	425	|	Too Early 	|	太早了	|
|	426	|	Upgrade Required 	|	需要升级	|
|	428	|	Precondition Required 	|	前提要求	|
|	429	|	Too Many Requests 	|	请求太多	|
|	431	|	Request Header Fields Too Large 	|	请求标头字段太大	|
|	451	|	Unavailable For Legal Reasons 	|	法律原因不可用	|
|	500	|	Internal Server Error 	|	内部服务器错误	|
|	501	|	Not Implemented 	|	未实现	|
|	502	|	Bad Gateway 	|	错误的网关	|
|	503	|	Service Unavailable 	|	暂停服务	|
|	504	|	Gateway Timeout 	|	网关超时	|
|	505	|	HTTP Version Not Supported 	|	不支持HTTP版本	|
|	506	|	Variant Also Negotiates 	|	服务器存在内部配置错	|
|	507	|	Insufficient Storage 	|	存储空间不足	|
|	508	|	Loop Detected 	|	检测到环路	|
|	510	|	Not Extended 	|	没有扩展	|
|	511	|	Network Authentication Required 	|	需要网络验证	|
