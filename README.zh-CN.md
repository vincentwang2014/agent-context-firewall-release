# Agent Context Firewall

[English](README.md)

**面向 AI 工具的本地数据防泄露防护：在内容到达外部模型之前完成检查。**

使用 AI 工具时，数据外泄往往不需要攻击者。一段含密钥的日志、一个存有卡号的文件，一旦进入对话，就已经发给了外部模型。Agent Context Firewall（ACF）在这一步之前介入。

## 核心能力

- **覆盖主要路径：** 保护提示词输入、工具调用、文件上传和本地文件读取，防止敏感内容泄露给外部模型。
- **按规则处置：** 发现敏感内容时，依据规则拦截，或交由用户决定。
- **重点加固：** 密钥、私钥等高敏感内容属于基本防护，在任何处理方式下都直接拦截。
- **透明可查：** ACF 的拦截和询问记录在检查日志中，并在 AI 工具的对话里说明原因。
- **灵活配置：** 规则包和单条规则可以开关，每个 AI 工具可以单独设置处理方式。
- **仅在本机运行：** 检查全部在本机完成，ACF 不会把内容发送给我们或任何第三方。

## 支持范围

**已支持**

| 类型 | 产品 | 运行环境 |
|---|---|---|
| AI 编程工具 | Claude Code、Codex | Windows 10 / 11、Linux（Debian/Ubuntu 系桌面）、macOS 13 及以上 |
| 桌面 AI 助手 | WorkBuddy | Windows 10 / 11、macOS 13 及以上 |
| 网页版 AI | claude.ai、ChatGPT、DeepSeek、Gemini：发送的消息和上传的文本文件 | Chrome、Edge（浏览器扩展） |

**计划支持**（计划中，以实际发布为准）

- OpenClaw
- 桌面聊天 App（探索中）

需要支持其他 AI 工具？请[告诉我们](mailto:agent.context.firewall@gmail.com)。

## 适用边界

- **防范对象：** ACF 针对的是疏忽和缺乏防护造成的泄露，前提是 AI 工具本身没有被劫持。
- **云端数据：** 在厂商云上运行的 AI 智能体读取云端账户时，内容不经过本机，ACF 无法检查。
- **未覆盖内容：** 图片和 PDF 中的文字不在检查范围内，桌面版聊天 App 目前不覆盖。
- **定位：** ACF 是一层防护，不应作为唯一的防护手段。

所有已知缺口都在[已知缺口文档](../../releases/tag/v0.4.0-beta.3)中列明，控制面板也会如实显示“目前不覆盖”。

## 下载

**当前版本：[0.4.0-beta.3](../../releases/tag/v0.4.0-beta.3)（测试版）。** 这是早期测试版，建议愿意帮我们测试、反馈问题的朋友安装。发布页有各系统的安装方法、签名指纹和这个版本的变化。

浏览器扩展：[Chrome 应用商店](https://chromewebstore.google.com/detail/pjghhjaabjmjfbnllcgnidmfpgecgfbk)。

这个仓库只放下载文件，不放源代码。

## 安装

| 系统 | 步骤 |
|---|---|
| **Windows 10 / 11** | 下载 `ACF-Setup.exe` 并运行。安装包暂无微软代码签名，系统可能提示风险。 |
| **macOS 13 及以上** | 下载 `.pkg`，双击安装，输入管理员密码。在终端运行 `acf panel` 打开控制面板。 |
| **Linux（Debian/Ubuntu 系桌面）** | 下载 `acf-0.4.0-beta.3-linux-amd64.tar.gz`，解压后在文件夹里运行 `sh install.sh`，它会先校验签名再安装。在终端运行 `acf panel` 打开控制面板。 |

如已安装旧版，请先卸载。

## 反馈

发邮件到 agent.context.firewall@gmail.com。控制面板里的“打包日志，发给我们”会生成一个可以附上的文件，里面只有 ACF 的检查记录，没有你的对话和文件内容。

隐私政策：[点击阅读](https://vincentwang2014.github.io/acf-privacy/)。
