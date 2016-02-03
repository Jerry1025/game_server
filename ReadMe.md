服务器是异步非阻塞多进程架构，分为LoginServer，GateServer，GameServer，MasterServer，DBServer，LogServer。
现将各个服务器大部分功能列出，供开发参考。

Robot:（测试机器人）
1、实现注册登录流程
2、与服务器正常通信，实现客户端逻辑

LoginServer:
客户端发送账号密码到LoginServer，LoginServer去AccountDb验证，验证失败断开连接，验证成功，则生成session，
根据玩家账号hash和gate在线人数选择gate，发送给客户端

GateServer:
接受客户端发过来的连接，向LoginServer进行session验证，同步在线玩家数量到LoginServer，转发消息到Game，Master

GameServer:
1、创建角色，角色登录，从DbServer加载数据返回给client
2、场景管理模块
3、Player模块
4、移动AOI模块
5、定时器管理模块
6、怪物AI模块
7、游戏逻辑

MasterServer：
1、管理GameServer，玩家在GameServer间跳转
2、存储在线玩家数据，进行相关校验验证，存储每个玩家对应的gameserver
3、存储公共数据，例如公会，好友信息
   
DbServer：
1、建立mongodb相关驱动和接口
2、建立存取数据接口

LogServer:
1、实现写日志文件相关接口
2、实现写Mysql操作流水相关接口

LogClient:
实现写日志相关接口，可供所有服务器调用

V8:
将V8引擎集成到项目中，V8执行环境，暴露C++接口给js，通过js编写游戏逻辑
