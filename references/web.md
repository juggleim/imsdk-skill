# Web 接入参考

本文件依据 Web [快速开始原文](原始文档/Web快速开始.md)及 SDK API 文档整理。接入时需要结合项目实际安装的 `jugglechat-websdk` 版本核对接口。

## 依赖与初始化

[依赖引入文档](原始文档/依赖引入.md)使用 `npm install jugglechat-websdk --save`，随后默认导入 `JIM`。快速开始以 Vue 为例；其他 Web 框架采用各自的应用生命周期管理 SDK 实例即可。

```js
import JIM from "jugglechat-websdk";

const jim = JIM.init({
  appkey: "<appKey>",
  serverList: ["<IM 服务地址>"],
});
```

服务地址由实际部署环境提供。快速开始中的示例域名和 Token 不是正式项目的配置值。

## 监听与 Token 连接

快速开始按以下顺序注册连接与消息监听，再用业务服务端签发的 Token 连接：

```js
const { Event, ConnectionState } = JIM;

jim.on(Event.STATE_CHANGED, ({ state, user }) => {
  if (state === ConnectionState.CONNECTED) {
    // 此时可以执行需要网络连接的 IM 操作
  }
});

jim.on(Event.MESSAGE_RECEIVED, (message) => {
  // 处理收到的消息
});

await jim.connect({ token: imToken });
```

完整示例见[Web 快速开始](原始文档/Web快速开始.md)，连接语义见[连接监听](原始文档/连接监听.mdx)。保持单个 SDK 实例和一组全局监听，避免组件反复挂载时重复注册。卸载方式以安装版本的 API 为准。SDK 处理常规断线重连；连接成功后再调用其他 IM 接口。

## 消息与会话

按目标功能读取[发送消息](原始文档/发送消息.md)、[消息监听](原始文档/消息监听.mdx)、[会话监听](原始文档/会话监听.mdx)、[历史消息](原始文档/历史消息.md)和[会话列表](原始文档/会话列表.md)的 JavaScript 选项卡。发送时使用 `jim.sendMessage(message, callbacks)`；核对项目安装版本的消息类型、事件常量和返回结构。
