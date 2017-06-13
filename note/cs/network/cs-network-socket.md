# res about computer science network socket #

## socket 连接过程 ##

1. 服务器监听
2. 客户端请求
3. 连接确认

## 常见API ##

int socket（int domain, int type, int protocol)

- **domain**:协议域（协议族），协议族决定了socket的地址类型，在通信中必须采用对应的地址格式。常见的协议族有：AF_INET（ipv4以及16位的端口号地址），AF_INET6,AF_UNIX, AF_ROUTE等。
- **type**：指定socket类型，常见的有SOCK_STREAM(流式socket，面向TCP应用)，SOCk_DGRAM（面向UDP应用），SOCK_PACKET,SOCK_SEQPACKET
- **protocol**：协议，常见的协议有IPPROTO_TCP，IPPROTO_UDP,IPPROTO_STCP,IPPROTO_TIPC

每种类型都有对应的协议，不能相互混淆。