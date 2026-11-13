# Agent Context Firewall

[English](README.md)

**给每个 AI 代理划清上下文的边界：哪些内容能进到哪个代理的上下文，哪些能通过工具发出去，哪些操作要先询问用户。**

AI 代理替你读文件、查资料、运行命令、调用工具，还会把任务分给子代理。这一路上，内容在你、代理、子代理、工具和外面的服务之间不断流动。数据外泄往往不需要攻击者：一段含密钥的日志被代理读到，就已经发给了 AI 模型背后的服务商；一份只该主代理看的资料被整段交给子代理，就多了一个不该看到它的地方。

Agent Context Firewall（ACF）装在你的电脑上，守在这些交接点上：内容跨过之前先检查，按规则放行、拦下或询问用户。密钥、密码、身份证件号、银行卡号这类规则包，是 ACF 在每道边界上判断的方式，不是产品本身。

## ACF 守的几道边界

1. **你 → 代理：** 你发给代理的消息，交给 AI 模型之前检查。
2. **文件、工具结果和检索资料 → 代理：** 代理读到的文件、命令结果、检索和其他工具的结果，交给 AI 模型之前检查；发现问题的内容不交给代理。
3. **父代理 → 子代理：** 交给子代理的任务说明，交出去之前检查；子代理自己读到的内容和交回的结果，同样检查。
4. **代理 → 外面：** 代理要运行的往外发数据的命令、外部工具（MCP）的参数、要打开的网址和搜索的关键词，运行之前检查。
5. **危险操作：** 要管理员权限的命令（`sudo`、`runas` 等），运行之前询问用户。
6. **ACF 自己：** 代理不能关掉或绕过 ACF：冲着 ACF 的命令和改动，任何情况下都拦下。

**基本防护：** 密钥、私钥这类最危险的内容，在每道边界上、任何处理方式下都拦下，不能关掉。

**方向：** 目标是每个代理只拿到它需要、也有权拿到的上下文。今天 ACF 按规则在每道边界检查内容；按代理的身份、任务和资料权限来判断（例如检索到的企业资料该不该交给这个代理），会随 SDK 和企业版接入。

各 AI 工具在每道边界上能做到哪一步，以控制面板和[已知保护缺口](#acf-看不到的地方)为准。

## 一切都在本机，一切都看得到

- 检查全部在你的电脑上完成，ACF 不把内容发给我们或任何第三方，也不保存对话文字。
- 每一次拦下和询问都会在 AI 工具的对话里说明原因，并记进控制面板的检查日志，带事件编号。
- 控制面板的每张 AI 工具卡片都列出：哪些已保护，哪些目前不覆盖，以及原因。
- 规则包和单条规则可以开关，每个 AI 工具可以单独选处理方式（基本防护除外）。

## ACF 看不到的地方

下面这些地方，内容可能进到 AI 模型而没有经过 ACF。多数是因为 AI 工具没有把内容交给检查程序，ACF 在本机补不上。

| 看不到的 | 原因 |
|---|---|
| AI 工具恢复或压缩对话时自己加入的历史、记忆和说明 | AI 工具没有在这些内容进入 AI 模型之前交给检查程序 |
| 子任务自动继承的父对话历史 | 目前没有任何受支持的 AI 工具让我们检查这份历史 |
| Claude Code 里用 `!` 直接运行的命令和输出 | Claude Code 没有为这条路提供检查点 |
| Claude Code 非自动模式下、以及 fork 子任务交回的报告 | Claude Code 只在自动模式、非 fork 子任务上提供检查点 |
| Codex 子任务交回的结果 | Codex 只让检查程序记录，不能在交回前拦下 |
| Codex 里命令、外部工具（MCP）和子任务以外的工具调用 | Codex 只把这几类交给检查程序 |
| 子代理该不该拿到某段内容、检索到的资料这个代理有没有权限看 | ACF 今天不知道代理的任务和资料的权限，只按规则判断内容（见上面的“方向”） |
| Codex 在服务商端运行的联网和检索工具 | 这些工具不在你的电脑上运行 |
| WorkBuddy 的命令输出 | WorkBuddy 不把命令输出交给检查程序 |
| WorkBuddy 回答过程中用“作为对话引导发送”发出的消息 | WorkBuddy 在这条路上没有执行 ACF 的拦下；已向它的开发方报告 |
| 图片、截图，以及 PDF、Office 文件和压缩包里的文字 | 我们还不能读这些文件的内容 |
| 云端 AI 智能体通过连接器读取 Gmail 这类云端账户 | 数据在云和云之间传输，不经过你的电脑 |
| Claude 桌面应用里的普通聊天 | 还没有接入；请改用网页版和 ACF 浏览器扩展 |

另外：

- ACF 假定 AI 工具不是恶意的。故意藏起来的命令、被劫持并有意隐藏的 AI 工具，不在保护范围内。
- ACF 自己出错时，内容会不经检查直接通过，让你的工作不被打断；对话里会有提示，控制面板会给出修复办法。
- 你同意以管理员身份运行的程序可以关掉 ACF；本机上的任何安全软件都是这样。
- ACF 是一层防护，不应作为唯一的防护。

完整清单见 [已知保护缺口](https://github.com/vincentwang2014/agent-context-firewall-release/releases/download/v0.4.0-beta.5/KNOWN_LIMITATIONS_zh.md)，每一条都写了对你的影响和你可以怎么做。

## 支持的 AI 工具和系统

| AI 工具 | Windows 10 / 11 | macOS 13 及以上 | Linux（Debian/Ubuntu 系桌面） |
|---|---|---|---|
| Claude Code | 支持 | 支持 | 支持 |
| Codex | 支持 | 支持 | 支持（含 ChatGPT 桌面版自带的 Codex） |
| WorkBuddy AI（国际版）和 WorkBuddy（中国版） | 支持 | 支持 | 已接入，还没有实测 |

网页 AI（claude.ai、ChatGPT、DeepSeek、Gemini）：用 Chrome 或 Edge 的 ACF 浏览器扩展，检查你发送的消息和上传的文本文件。

- ACF 的询问窗口目前只有 Windows 上有。在 Linux 和 macOS 上，规则要求询问用户时（包括要管理员权限的命令），Claude Code 在需要确认的权限模式下用它自己的确认框询问，其他情况多数改为拦下，对话里说明原因。
- macOS 版目前只在 Apple 芯片的 macOS 14 上测试过。

计划接入：OpenClaw 等。需要支持别的 AI 工具，[告诉我们](mailto:agent.context.firewall@gmail.com)。

## 下载和安装

**当前版本：[0.4.0-beta.5](../../releases/tag/v0.4.0-beta.5)（测试版）。** 这是早期测试版，给愿意试用并反馈的朋友。发布页有每个系统的安装步骤、签名指纹和本版的改动。

| 系统 | 下载 | 安装 |
|---|---|---|
| Windows 10 / 11 | [ACF-Setup.exe](https://github.com/vincentwang2014/agent-context-firewall-release/releases/download/v0.4.0-beta.5/ACF-Setup.exe) | 运行它。安装程序还没有微软代码签名，Windows 可能会提示风险。 |
| macOS 13 及以上 | [acf-0.4.0-beta.5-mac-universal.pkg](https://github.com/vincentwang2014/agent-context-firewall-release/releases/download/v0.4.0-beta.5/acf-0.4.0-beta.5-mac-universal.pkg) | 双击，按提示操作，输入管理员密码。安装包经过 Apple 公证。 |
| Linux（amd64） | [acf-0.4.0-beta.5-linux-amd64.run](https://github.com/vincentwang2014/agent-context-firewall-release/releases/download/v0.4.0-beta.5/acf-0.4.0-beta.5-linux-amd64.run) | 在下载文件夹打开终端，运行 `sh acf-0.4.0-beta.5-linux-amd64.run`。它先核对签名，再安装。 |

装好后控制面板会自己打开。以后从开始菜单、启动台或应用菜单打开“ACF 控制面板”，也可以在终端运行 `acf panel`（macOS、Linux）。

已经装有旧版时，直接安装新版即可：会更新，设置保留。

浏览器扩展：[Chrome 应用商店](https://chromewebstore.google.com/detail/pjghhjaabjmjfbnllcgnidmfpgecgfbk)。

本仓库只提供下载，不含源代码。

## 反馈

发邮件到 agent.context.firewall@gmail.com。控制面板里的“打包日志发给我们”会生成一个文件，可以附上；它只含 ACF 的检查记录，不含你的对话和文件。

隐私政策：[点此查看](https://vincentwang2014.github.io/acf-privacy/)。
