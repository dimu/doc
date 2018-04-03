# spring security oauth2 研究
OAuth的核心思想：让客户端安全可控的获取用户的授权，与服务提供者进行信息交互。

## 权限管理相关技术

## oauth2的给予客户端授权的4种模式
参考[http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html](http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html "授权码分配四种模式")
### authorization code(授权码模式)

### implicit（简化模式）

### resource owner password credentials（密码模式）

### client credentials(客户端模式)

## spring相关默认端点

## token store（token存储模式）

### InMemoryTokenStore

### JdbcTokenStore

### JwtTokenStore

### RedisTokesnStore

## authentication(技术方式)
### In-Memory Authentication

### JDBC Authentication

### LDAP Authentication

### AuthenticationProvider

### UserDatailsService

## ResourceServer实现方式

### ResourceServer如何与zuul配合使用

## zuul与oauth2结合


