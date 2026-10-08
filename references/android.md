# Android 接入参考

本文件依据 Android SDK 的 `JIM.java`、`IConnectionManager.java`、`IMessageManager.java`，以及演示工程整理。文件名是来源线索，使用 skill 不依赖这些仓库位于本机。

## 依赖与初始化

[依赖引入文档](原始文档/依赖引入.md)给出 Maven 仓库 `https://repo.juggle.im/repository/maven-releases/` 和示例坐标 `com.juggle.im:juggle:1.8.13.2`。版本号属于文档快照，接入时核对项目要用的版本。

[初始化文档](原始文档/初始化.mdx)和演示工程均先设置服务地址，再初始化单例。以下片段保留演示工程的调用顺序，并用占位值替换测试配置：

```kotlin
val serverList = listOf("<IM 服务地址>")
JIM.getInstance().setServerUrls(serverList)
JIM.getInstance().init(this, "<appKey>")
```

## Token 连接与监听

演示工程 `LoginActivity.kt` 在页面创建时注册连接监听，从业务登录响应取得 `im_token` 后连接，并在页面销毁时移除监听：

```kotlin
private val listenerKey = "login"

// 页面创建时，this 实现 IConnectionStatusListener
JIM.getInstance().connectionManager.addConnectionStatusListener(listenerKey, this)

// 业务服务端登录成功后
JIM.getInstance().connectionManager.connect(imToken)

// 页面销毁时
JIM.getInstance().connectionManager.removeConnectionStatusListener(listenerKey)
```

`onDbOpen()` 表示本地数据库可用；`onStatusChange()` 收到 `JIMConst.ConnectionStatus.CONNECTED` 才表示网络连接可用于发送。连接失败时查看回调错误码。详见[连接文档](原始文档/连接.mdx)和[连接监听文档](原始文档/连接监听.mdx)。

## 消息与会话

按目标功能读取[发送消息](原始文档/发送消息.md)、[消息监听](原始文档/消息监听.mdx)、[会话监听](原始文档/会话监听.mdx)、[历史消息](原始文档/历史消息.md)和[会话列表](原始文档/会话列表.md)的 Android 选项卡。消息发送通常经 `JIM.getInstance().getMessageManager()`，会话操作经 `getConversationManager()`；以项目安装版本的接口定义核对参数及回调。
