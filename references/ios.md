# iOS 接入参考

本文件依据 iOS SDK 的 `JIM.h`、`JConnectionProtocol.h`，以及演示工程整理。文件名是来源线索，使用 skill 不依赖这些仓库位于本机。

## 依赖与初始化

[依赖引入文档](原始文档/依赖引入.md)给出 CocoaPods 示例：`pod 'JuggleIM', '1.8.52.4'`，随后执行 `pod install`。版本号属于文档快照，接入时核对项目要用的版本。

演示工程在 `AppDelegate.swift` 中先设置 IM 服务地址，再初始化：

```swift
JIM.shared().setServerUrls(["<IM 服务地址>"])
JIM.shared().initWithAppKey("<appKey>")
```

这与[初始化文档](原始文档/初始化.mdx)的调用顺序一致。演示工程随后还注册自定义消息类型、推送 Token 和通话引擎；仅在相应功能需要时接入。

## Token 连接与监听

演示工程在业务登录成功并获得 Token 后调用：

```swift
JIM.shared().connectionManager.connect(withToken: imToken)
```

Objective-C API 在 `JConnectionProtocol.h` 中声明为 `connectWithToken:`。同一协议还提供 `addDelegate:` 等连接监听接口。`dbDidOpen` 表示本地数据库可用；连接状态变为 `JConnectionStatusConnected` 后才可发送。具体回调见[连接文档](原始文档/连接.mdx)和[连接监听文档](原始文档/连接监听.mdx)。若项目采用 Swift，按安装版本核对 Objective-C 方法的 Swift 映射名称。

## 消息与会话

按目标功能读取[发送消息](原始文档/发送消息.md)、[消息监听](原始文档/消息监听.mdx)、[会话监听](原始文档/会话监听.mdx)、[历史消息](原始文档/历史消息.md)和[会话列表](原始文档/会话列表.md)的 iOS 选项卡。`JIM.shared().messageManager` 与 `conversationManager` 是相应入口；以项目安装版本的 `JMessageProtocol.h`、`JConversationProtocol.h` 核对参数、代理和回调。
