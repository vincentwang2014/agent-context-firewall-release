# Agent Context Firewall

[English](README.md)

在你自己的电脑上，在 AI 工具把内容发出去之前先检查一遍。发现密钥、密码、卡号这类不该外泄的东西，按规则拦下，或者询问用户。你写的、打开的内容都不会发给我们或任何人。

这个仓库只放下载文件，不放源代码。

## 两个部分

| 部分 | 检查什么 | 怎么获取 |
|---|---|---|
| **ACF（AI 工具版，Windows、Linux、macOS）** | Claude Code、Codex、WorkBuddy：你发的消息、交给子任务的内容、AI 读到的内容、往外发的命令 | **[0.4.0-beta.3](../../releases/tag/v0.4.0-beta.3)**，各系统的获取方式见下 |
| **ACF 浏览器扩展** | 网页版 AI：claude.ai、ChatGPT、DeepSeek、Gemini：你发出的消息和上传的文本文件 | [Chrome 应用商店](https://chromewebstore.google.com/detail/pjghhjaabjmjfbnllcgnidmfpgecgfbk)（Edge 也能装） |

> **测试版。** 0.4.0-beta.3 是早期测试版。只建议愿意帮我们测试、反馈问题的朋友安装，不要把它当作唯一的防护。安装前请先看[发布页](../../releases/tag/v0.4.0-beta.3)上的更新说明和已知缺口。

## 按系统获取

三个系统都在 [0.4.0-beta.3 发布页](../../releases/tag/v0.4.0-beta.3)。

**Windows 10 / 11。** 下载 `ACF-Setup.exe` 并运行。如果装着旧版 ACF，请先卸载。它还没有微软代码签名，Windows 和杀毒软件可能会提示风险。ACF 和规则包会自己更新。

**Linux（Debian/Ubuntu 系桌面）。** 下载 `acf` 和 `acf-panel-runtime` 两个 `.deb` 安装包、它们的 `.asc` 签名、`verify_deb_gpgv.sh` 和 `acf-linux-deb-release-keyring.gpg`。用 `./verify_deb_gpgv.sh 安装包.deb 安装包.deb.asc` 逐个核对，再用 `sudo apt install ./acf-panel-runtime_*.deb ./acf_*.deb` 一起安装。在终端运行 `acf panel` 打开控制面板。要更新时，安装新的安装包。

安装包用我们的 Linux OpenPGP 发布密钥签名：

- 主密钥：`C66A95EDE3C9A2ECF569D43216B5E948DEDC6180`
- 签名子密钥：`A72107565CE6F382964F9EAEB52235D40CC4CD23`

**macOS 13 及以上（Apple 芯片或 Intel；只在 Apple 芯片上测试过）。** 下载签名的 `.pkg`，打开并输入管理员密码。在终端运行 `acf panel` 打开控制面板。要更新时，先运行 `acf uninstall`，再打开新的安装包。

## 发现问题时会怎样

- **拦下：** 密钥、私钥这类东西不会发出去，AI 工具的对话里（或网页上）会说明原因。
- **询问用户：** 卡号这类内容，在 Windows 上 ACF 会弹出自己的确认窗口，你点了才放行。Linux 和 macOS 上这个窗口还没做好：Claude Code 在运行工具之前用它自己的确认框询问，其他内容直接拦下。
- **ACF 看不到的地方**（桌面版聊天 App、在厂商云上运行的 AI 智能体、图片和 PDF 里的内容），已知缺口和控制面板里都如实写明。

## 反馈

发邮件到 agent.context.firewall@gmail.com。控制面板里的"打包日志，发给我们"会生成一个可以附上的文件，里面只有 ACF 的检查记录，没有你的对话和文件内容。

隐私政策：[点击阅读](https://vincentwang2014.github.io/acf-privacy/)。

## 早期下载

`v0.1.x-dev` 那几个版本是浏览器扩展的早期开发预览版，留作记录。请改用 Chrome 应用商店的版本。
