#Glob-proxy.js

在工作中，经常遇见一个问题，服务端的开发总是比前端开发要慢很多，于是我们需要在本地模拟数据，但是现实往往让我们出人意料，我的数据模拟可能在另一个环境中，而我的开发环境，需要请求数据时，就发生了跨域的问题。而且，来来回回在改地址，我会非常的纠结，于是写下了这个，基于nodejs的web代理，来对请求进行处理。下午抽了些时间，对代码进行了整理，现在仅支持对GET POST的代理。

## Download
源代码可以在[Github](https://github.com/lcepy/glob-proxy)上进行下载，也可以使用npm包管理器进行安装

	npm install glob-proxy
## Use

	var glob = require('glob-proxy');
	glob.Config({
	'PORT':'8084',
	'REQUEST':{
		'GET':{
			'/github':'/mock.json'
		},
		'POST':{
			'/github':'/mock.json',
			'/django':'http://restapi.cruises/CruiseService.svc/GetBookingInfo'
		}
	},
	'TYPE':'HTTP',
	'ROOT':'D:\\Github'
	});

## Config

>
>PORT start server port 启动服务器端口号
>
>TYPE 处理请求时，按什么类型来处理	
>
>ROOT 配置读取本地文件的跟目录
>
>REQUEST 配置请求映射
>
>GET POST 请求
>

默认开启请求代理，一个真实的请求将根据请求映射，请求出去。如果需要读取本地文件，在URL中加上?local=xx，把local参数开启为true即可，如果元数据想使用mock来构建，则在URL中加上mock=xx，把mock参数开启为true。

默认对远程请求启用内存缓存机制，并对第一次请求生成一个.txt物理缓存文件。当URL 参数变化时，会更新内存中已经缓存的对象，并再按时间生成一个.txt物理缓存文件。


未来改进：

	
1. 支持restful风格的其他method，如PUT DELETE
2. 支持从后台提交SOAP
3. 指定静态资源






