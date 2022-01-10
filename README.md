# study skynet
## 1.Clone 源码
git clone https://github.com/cloudwu/skynet.git
## 2.编译源码
make linux
## 3.运行第一个服务器skynet节点
$ ./skynet examples/config  
## 4.运行第一个客户端
$ ./3rd/lua/lua examples/client.lua  这里要用5.4的Lua版本，否则要报错
## 5.构建服务的基础API
local skynet = require "skynet" 

--conf配置信息已经写入到注册表中，通过该函数获取注册表的变量值
skynet.getenv(varName) 
--设置注册表信息，varValue一般是number或string，但是不能设置已经存在的varname
skynet.setenv(varName, varValue) 
--打印函数
skynet.error(...)
--用 func 函数初始化服务，并将消息处理函数注册到 C 层，让该服务可以工作。
skynet.start(func) 
--若服务尚未初始化完成，则注册一个函数等服务初始化阶段再执行；若服务已经初始化完成，则立刻运行该函数。
skynet.init(func) 
--结束当前服务
skynet.exit() 
--获取当前服务的句柄handler
skynet.self()
--将handle转换成字符串
skynet.address(handler)
--退出skynet进程
require "skynet.manager"   --除了需要引入skynet包以外还要再引入skynet.manager包。
skynet.abort()
--强制杀死其他服务
skynet.kill(address) --可以用来强制关闭别的服务。但强烈不推荐这样做。因为对象会在任意一条消息处理完毕后，毫无征兆的退出。所以推荐的做法是，发送一条消息，让对方自己善后以及调用 skynet.exit 。注：skynet.kill(skynet.self()) 不完全等价于 skynet.exit() ，后者更安全。
##
