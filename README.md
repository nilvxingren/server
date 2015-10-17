# AOAS 通用服务端
AOAS是一个快速开发系统模板, 基于角色授权体系. 

整个系统以JSON格式来交互数据, 前台传过来的内容也是JSON格式字符串, 而非传统的form字段. 如在js端传过来的, 可用JSON.stringify(xxx)来格式后再传过来.

为了方便移动端调用, 未用session功能, 而是用了`jwt token`

### 新增功能模块
若要增加模块功能. 可按如下步骤来操作.

* 在`models`目录增加新的model. 并在models/base.go下的`SyncTables`方法里增加新model的名字, 以便同步数据结构到数据库.
* 在`controllers`目录增加对应的操作控制器. 可继承Base这个控制器. 里面会带几个可能会用到的对象. 如logger, dbengine, config. 有某些清空下可能要用到config中的某些值.
可在新的controller里写init方法. 把可能用到的权限写进去, 以便后续做授权操作.
* 在routers/router.go里增对应的路由连接. 

调试时可用建议用[gin](https://github.com/codegangsta/gin)这类的控件, 以便实时刷新变动. 

### 调用API
当客户端调用时, 可以进行login操作拿到 `token`. 并在后续http调用时增加如下header.   

```http
Authorization: Bearer {{your token}}
```

### 用到的库   
* [gin](https://github.com/gin-gonic/gin) http framework
* [xorm](https://github.com/go-xorm/xorm) 数据库orm   
* [toml](https://github.com/BurntSushi/toml) 解析config
* [jwt-go](https://github.com/dgrijalva/jwt-go) 生成token相关

### 工具推荐
调试调用API时, 我推荐 [Insomnia](http://insomnia.rest/), 整个用下来非常不错. 尤其支持变量及组功能相对有用.