# Agent Context Firewall

[English](README.md)

在你自己的电脑上，在 AI 工具把内容发出去之前先检查一遍。发现密钥、密码、卡号这类不该外泄的东西，按规则拦下，或者先问你。你写的、打开的内容都不会发给我们或任何人。

这个仓库只放下载文件，不放源代码。

## 两个部分

| 部分 | 检查什么 | 怎么获取 |
|---|---|---|
| **ACF（AI 工具版，Windows）** | Claude Code、Codex（命令行版和桌面版）、WorkBuddy：你发的消息、交给子任务的内容、AI 读到的内容、往外发的命令 | **[0.4.0-beta.2](https://github.com/vincentwang2014/agent-context-firewall-release/releases/tag/v0.4.0-beta.2)**（点这里下载） |
| **ACF 浏览器扩展** | 网页版 AI：claude.ai、ChatGPT、DeepSeek、Gemini：你发出的消息和上传的文本文件 | [Chrome 应用商店](https://chromewebstore.google.com/detail/pjghhjaabjmjfbnllcgnidmfpgecgfbk)（Edge 也能装） |

> **测试版。** 0.4.0-beta.2 是早期测试版，没有微软代码签名，Windows 和杀毒软件可能会提示风险。只建议愿意帮我们测试、反馈问题的朋友安装，不要把它当作唯一的防护。安装前请先看 Release 里的 `README_zh.txt`。
>
> **装过 0.4.0-beta.1？** 请先卸载它（设置 → 应用 → 已安装的应用 → Agent Context Firewall → 卸载），再运行新的 `ACF-Setup.exe`。beta.1 已过时。
>
> 这个测试版只有 Windows 版（Windows 10 / 11）。macOS 和 Linux 版正在准备，发布时会另行通知。

## 发现问题时会怎样

- **拦下：** 密钥、私钥这类东西不会发出去，AI 工具的对话里（或网页上）会说明原因。
- **先问你：** 卡号这类内容，ACF 会弹出自己的确认窗口，你点了才放行。
- **ACF 看不到的地方**（桌面版聊天 App、在厂商云上运行的 AI 智能体、图片和 PDF 里的内容），测试说明和控制面板里都如实写明。

## 反馈

发邮件到 agent.context.firewall@gmail.com。控制面板里的"打包日志，发给我们"会生成一个可以附上的文件，里面只有 ACF 的检查记录，没有你的对话和文件内容。

隐私政策：[点击阅读](https://vincentwang2014.github.io/acf-privacy/)。

## 早期下载

`v0.1.x-dev` 那几个版本是浏览器扩展的早期开发预览版，留作记录。请改用 Chrome 应用商店的版本。
