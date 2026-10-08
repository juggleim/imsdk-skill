# JuggleIM SDK 集成 Skill

面向开发者的 JuggleIM SDK 集成指引，支持 **Android、iOS 和 Web**。当你需要在现有应用中接入 IM，或排查初始化、Token 连接、监听、消息和会话问题时，可以让支持 Skill 的编码助手使用本仓库。

## 安装

推荐使用 [Skills CLI](https://github.com/vercel-labs/skills) 安装。需要 Node.js 和 npx；运行后选择使用的编码助手。以下命令安装到用户级目录，供所有项目使用：

```bash
npx skills add juggleim/imsdk-skill -g
```

如果只想在当前项目中使用，去掉 `-g`：

```bash
npx skills add juggleim/imsdk-skill
```

也可以不依赖 Skills CLI，先克隆仓库，再把整个目录放入所用编码助手指定的 skills 目录，确保目录下直接包含 `SKILL.md` 和 `references/`：

```bash
git clone https://github.com/juggleim/imsdk-skill.git
```

Skill 遵循目录式 Agent Skills 结构，不限定编码助手。安装位置和显式调用方式以所用工具的说明为准。

## 使用

在开发项目中描述目标平台与任务，例如：

> 请使用 integrate-juggle-im-sdk，在 Android 项目中接入 JuggleIM，完成初始化、Token 连接和文本消息收发。

使用前准备好应用标识、实际部署的 IM 服务地址，以及由业务服务端签发的用户 IM Token。Skill 会先检查目标项目已安装的 SDK 版本，再按平台查阅参考资料；示例中的版本号和配置值不能直接当作生产环境配置。

## 仓库内容

| 路径 | 用途 |
| --- | --- |
| [SKILL.md](SKILL.md) | 触发条件、资料选择与集成流程 |
| [references/android.md](references/android.md) | Android SDK 和演示工程中的接入入口 |
| [references/ios.md](references/ios.md) | iOS SDK 和演示工程中的接入入口 |
| [references/web.md](references/web.md) | Web 快速开始与相关 API 的接入入口 |
| [references/原始文档](references/原始文档) | 依赖、初始化、连接、监听、消息、会话等文档快照 |

参考资料来自 JuggleIM 的客户端文档、Android SDK 与 demo、iOS SDK 与 QuickStart。Web 平台以官方文档中的快速开始示例为依据。文档快照便于离线阅读；对于新增功能或版本差异，请以[官网文档](https://juggle.im/docs/guide/intro/)和项目实际安装版本的 API 为准。

## 许可证

本仓库采用 [Apache License 2.0](LICENSE)。
