# Agent Context Firewall

[中文](README.zh-CN.md)

**Local data-leak protection for AI tools: content is checked before it reaches an external model.**

With AI tools, a data leak often needs no attacker. Once a log containing a key or a file holding a card number enters a conversation, it has already gone to an external model. Agent Context Firewall (ACF) steps in before that point.

## Core capabilities

- **Covers the main paths:** prompts, tool calls, file uploads and local file reads, to keep sensitive content from leaking to external models.
- **Rule-based handling:** when sensitive content is found, ACF blocks it according to the rules or leaves the decision to the user.
- **Hardened for the most sensitive data:** keys, private keys and the like fall under basic protection and are blocked in every handling mode.
- **Transparent:** ACF's blocks and asks are recorded in the Inspection log and explained in the AI tool's conversation.
- **Configurable:** rule packs and single rules can be switched, and each AI tool can have its own handling.
- **Runs locally:** all checks happen on the computer. ACF doesn't send content to us or to any third party.

## Coverage

**Supported**

| Type | Product | Runs on |
|---|---|---|
| AI coding tools | Claude Code, Codex | Windows 10 / 11, Linux (Debian/Ubuntu-family desktops), macOS 13 or later |
| Desktop AI assistant | WorkBuddy | Windows 10 / 11, macOS 13 or later |
| Web AI | claude.ai, ChatGPT, DeepSeek, Gemini: messages you send and text files you upload | Chrome, Edge (browser extension) |

**Planned** (subject to change; what ships is what counts)

- OpenClaw
- Desktop chat apps (being explored)

Need another AI tool supported? [Tell us](mailto:agent.context.firewall@gmail.com).

## Scope and limits

- **Threat model:** ACF addresses leaks caused by oversight and missing safeguards, and assumes the AI tool itself hasn't been hijacked.
- **Cloud data:** when an AI agent on a vendor's cloud reads cloud accounts, the content doesn't pass through the computer, so ACF can't check it.
- **Content not covered:** text in images and PDFs isn't checked, and desktop chat apps aren't covered yet.
- **Positioning:** ACF is one layer of protection, not the only one to rely on.

All known gaps are listed in the [known limitations](../../releases/tag/v0.4.0-beta.3), and the control panel shows "Not covered yet" where that applies.

## Download

**Current version: [0.4.0-beta.3](../../releases/tag/v0.4.0-beta.3) (beta).** This is an early beta, meant for friends willing to test it and send feedback. The release page has the install steps for each system, signature fingerprints and what changed in this version.

Browser extension: [Chrome Web Store](https://chromewebstore.google.com/detail/pjghhjaabjmjfbnllcgnidmfpgecgfbk).

This repository holds downloads only, not source code.

## Install

| System | Steps |
|---|---|
| **Windows 10 / 11** | Download `ACF-Setup.exe` and run it. It has no Microsoft code signature yet, so Windows may warn you. |
| **macOS 13 or later** | Download the `.pkg`, double-click it and enter your administrator password. Run `acf panel` in a terminal to open the control panel. |
| **Linux (Debian/Ubuntu-family desktops)** | Download `acf-0.4.0-beta.3-linux-amd64.run`, open a terminal in the download folder and run `sh acf-0.4.0-beta.3-linux-amd64.run`. It checks the signatures, installs, and opens the control panel. Afterwards, run `acf panel` in a terminal to open it. |

If an older version is installed, uninstall it first.

## Feedback

Email agent.context.firewall@gmail.com. "Pack logs to send us" in the control panel makes a file you can attach. It holds only ACF's inspection records, not your conversations or files.

Privacy policy: [read it here](https://vincentwang2014.github.io/acf-privacy/).
