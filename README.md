# Agent Context Firewall

[中文](README.zh-CN.md)

Checks what your AI tools are about to send, on your own computer, before it is sent. When it finds something that shouldn't leave your computer, such as a key, a password or a card number, it blocks it or asks you first. Nothing you write or open is sent to us or anyone else.

This repository has downloads only (no source code).

## Two parts

| Part | For | Get it |
|---|---|---|
| **ACF for AI tools** (Windows) | Claude Code, Codex (command line and desktop), WorkBuddy: your messages, what is handed to subtasks, what the AI reads, outgoing commands | **0.4.0-beta.1**, see [Releases](../../releases) |
| **ACF browser extension** | AI websites: claude.ai, ChatGPT, DeepSeek, Gemini: the message you send and the text files you upload | [Chrome Web Store](https://chromewebstore.google.com/detail/pjghhjaabjmjfbnllcgnidmfpgecgfbk) (also installable in Edge) |

> **Beta.** 0.4.0-beta.1 is an early test version without a Microsoft code signature; Windows and antivirus software may warn you. It is for friends who are willing to test it and send feedback, not as your only protection. Read `README_en.txt` in the release before installing.
>
> This beta is for Windows only (Windows 10 / 11). macOS and Linux versions are in preparation; we'll announce them when they're ready.

## What happens when ACF finds something

- **Blocked:** keys, private keys and similar secrets are not sent; the AI tool's conversation (or the page) says why.
- **Asks you first:** for things such as card numbers, ACF shows its own confirmation window; only your click lets it through.
- **What ACF can't see** (desktop chat apps, AI agents running in a vendor's cloud, images and PDFs) is listed honestly in the tester notes and the Control Panel.

## Feedback

Email agent.context.firewall@gmail.com. In the Control Panel, "Pack logs to send us" creates a file you can attach; it holds ACF's check records only, never your conversations or file contents.

Privacy policy: [read it](https://vincentwang2014.github.io/acf-privacy/).

## Older downloads

The `v0.1.x-dev` releases are early development previews of the browser extension, kept for reference. Please use the Chrome Web Store version instead.
