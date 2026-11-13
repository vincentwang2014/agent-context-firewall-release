# Agent Context Firewall

[中文](README.zh-CN.md)

**Context boundaries for every AI agent: what may get into which agent's context, what may leave through tool calls, and which operations ask the user first.**

AI agents read files, look things up, run commands and call tools for you, and hand parts of the work to sub-agents. Along the way, content keeps moving between you, agents, sub-agents, tools and outside services. A data leak often needs no attacker: once an agent reads a log with a key in it, the key has already gone to the provider behind the AI model; once a document only the main agent should see is handed whole to a sub-agent, one more place has it that shouldn't.

Agent Context Firewall (ACF) runs on your computer and sits at these handoff points: it checks content before it crosses, then lets it through, blocks it or asks the user, according to the rules. Rule packs for keys, passwords, identity numbers and card numbers are how ACF decides at each boundary; they are not the product itself.

## The boundaries ACF guards

1. **You → agent:** the messages you send an agent are checked before they reach the AI model.
2. **Files, tool results and retrieved content → agent:** files, command results, retrieval and other tool results an agent reads are checked before they reach the AI model; content with a problem isn't handed to the agent.
3. **Parent agent → sub-agent:** the task a sub-agent is given is checked before it is handed over; what the sub-agent reads itself and what it hands back are checked too.
4. **Agent → outside:** commands an agent runs that send data out, external tool (MCP) arguments, URLs to open and search terms are checked before they run.
5. **Risky operations:** commands that need administrator rights (`sudo`, `runas` and the like) are asked about before they run.
6. **ACF itself:** an agent can't switch ACF off or get around it: commands and changes aimed at ACF are blocked in every case.

**Basic protection:** the most dangerous content, such as keys and private keys, is blocked at every boundary in every handling mode, and can't be turned off.

**Direction:** the goal is that each agent gets only the context it needs and is allowed to have. Today ACF checks content by rules at each boundary; judging by the agent's identity, task and data permissions (for example, whether a retrieved company document should go to this agent) will come with the SDK and the enterprise edition.

How far each AI tool goes at each boundary is shown in the control panel and in [what ACF can't see](#what-acf-cant-see).

## Everything stays local, and everything is shown

- All checks happen on your computer. ACF doesn't send content to us or to any third party, and doesn't keep conversation text.
- Every block and ask is explained in the AI tool's conversation and recorded in the control panel's Inspection log, with an event number.
- Each AI tool card in the control panel lists what is protected, what isn't covered yet, and why.
- Rule packs and single rules can be switched on and off, and each AI tool can have its own handling (basic protection excepted).

## What ACF can't see

In these places, content may get into the AI model without passing through ACF. Most of them are there because the AI tool doesn't hand the content to the checker, and ACF can't make up for that on the computer.

| Not seen | Why |
|---|---|
| History, memory and instructions the AI tool adds itself when it resumes or compacts a conversation | The AI tool doesn't hand this content to the checker before it goes into the AI model |
| Parent conversation history a subtask inherits automatically | None of the supported AI tools lets us check it |
| Commands you run with `!` in Claude Code, and their output | Claude Code offers no check point on this path |
| Reports from Claude Code subtasks outside auto mode, and from fork subtasks | Claude Code offers a check point only in auto mode, for non-fork subtasks |
| Results Codex subtasks hand back | Codex lets the checker record them only, not stop them before they return |
| Codex tool calls other than commands, external tools (MCP) and subtasks | Codex hands only these kinds to the checker |
| Whether a sub-agent should get a piece of content, or whether this agent may see a retrieved document | ACF doesn't know an agent's task or a document's permissions yet and judges content by rules only (see "Direction" above) |
| Codex web and retrieval tools that run at the provider | These tools don't run on your computer |
| WorkBuddy command output | WorkBuddy doesn't hand command output to the checker |
| Messages sent with "send as conversation guidance" while WorkBuddy is answering | WorkBuddy doesn't apply ACF's block on this path; we have reported it to its developer |
| Images, screenshots, and text inside PDFs, Office files and archives | We can't read the content of these files yet |
| Cloud AI agents reading cloud accounts such as Gmail through connectors | The data moves from cloud to cloud and never passes through your computer |
| Ordinary chat in the Claude desktop app | Not connected yet; use the web version with the ACF browser extension |

Also:

- ACF assumes the AI tool isn't malicious. Deliberately hidden commands, and a hijacked AI tool that hides what it does, are out of scope.
- If ACF itself fails, content passes unchecked so your work isn't interrupted; the conversation shows a notice and the control panel offers a fix.
- A program you allow to run as administrator can turn ACF off; that is true of any security software on the computer.
- ACF is one layer of protection, not the only one to rely on.

The full list is in the [known limitations](https://github.com/vincentwang2014/agent-context-firewall-release/releases/download/v0.4.0-beta.5/KNOWN_LIMITATIONS_en.md); each entry says what it means for you and what you can do.

## Supported AI tools and systems

| AI tool | Windows 10 / 11 | macOS 13 or later | Linux (Debian/Ubuntu-family desktops) |
|---|---|---|---|
| Claude Code | Supported | Supported | Supported |
| Codex | Supported | Supported | Supported (including the Codex built into the ChatGPT desktop app) |
| WorkBuddy AI (international) and WorkBuddy (China edition) | Supported | Supported | Connected, not yet tested |

Web AI (claude.ai, ChatGPT, DeepSeek, Gemini): the ACF browser extension for Chrome and Edge checks the messages you send and the text files you upload.

- ACF's ask window exists only on Windows so far. On Linux and macOS, when a rule asks the user (including commands that need administrator rights), Claude Code asks in its own dialog in permission modes that confirm; otherwise the content is mostly blocked instead and the conversation says why.
- The macOS version has been tested only on macOS 14 on Apple chips so far.

Planned: OpenClaw and others. Need another AI tool supported? [Tell us](mailto:agent.context.firewall@gmail.com).

## Download and install

**Current version: [0.4.0-beta.5](../../releases/tag/v0.4.0-beta.5) (beta).** This is an early beta, meant for friends willing to test it and send feedback. The release page has the install steps for each system, signature fingerprints and what changed in this version.

| System | Download | Install |
|---|---|---|
| Windows 10 / 11 | [ACF-Setup.exe](https://github.com/vincentwang2014/agent-context-firewall-release/releases/download/v0.4.0-beta.5/ACF-Setup.exe) | Run it. It has no Microsoft code signature yet, so Windows may warn you. |
| macOS 13 or later | [acf-0.4.0-beta.5-mac-universal.pkg](https://github.com/vincentwang2014/agent-context-firewall-release/releases/download/v0.4.0-beta.5/acf-0.4.0-beta.5-mac-universal.pkg) | Double-click it, follow the steps and enter an administrator password. The package is notarized by Apple. |
| Linux (amd64) | [acf-0.4.0-beta.5-linux-amd64.run](https://github.com/vincentwang2014/agent-context-firewall-release/releases/download/v0.4.0-beta.5/acf-0.4.0-beta.5-linux-amd64.run) | Open a terminal in the download folder and run `sh acf-0.4.0-beta.5-linux-amd64.run`. It checks the signatures, then installs. |

The control panel opens by itself when installation is done. Later, open "ACF Control Panel" from the Start menu, Launchpad or the applications menu, or run `acf panel` in a terminal (macOS, Linux).

If an older version is installed, just install over it: it is updated and your settings are kept.

Browser extension: [Chrome Web Store](https://chromewebstore.google.com/detail/pjghhjaabjmjfbnllcgnidmfpgecgfbk).

This repository holds downloads only, not source code.

## Feedback

Email agent.context.firewall@gmail.com. "Pack logs to send us" in the control panel makes a file you can attach. It holds only ACF's inspection records, not your conversations or files.

Privacy policy: [read it here](https://vincentwang2014.github.io/acf-privacy/).
