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

| Product | Protects | Runs on |
|---|---|---|
| **ACF** | Claude Code, Codex, WorkBuddy | Windows 10 / 11, Linux (Debian/Ubuntu-family desktops), macOS 13 or later |
| **ACF browser extension** | Web claude.ai, ChatGPT, DeepSeek, Gemini: the messages you send and the text files you upload | Chrome, Edge |

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

## Feedback

Email agent.context.firewall@gmail.com. "Pack logs to send us" in the control panel makes a file you can attach. It holds only ACF's inspection records, not your conversations or files.

Privacy policy: [read it here](https://vincentwang2014.github.io/acf-privacy/).
