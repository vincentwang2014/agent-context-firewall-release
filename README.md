# Agent Context Firewall

[中文](README.zh-CN.md)

Checks what your AI tools are about to send, on your own computer, before it is sent. When it finds something that shouldn't leave your computer, such as a key, a password or a card number, it blocks it or asks you first. Nothing you write or open is sent to us or anyone else.

This repository has downloads only (no source code).

## Two parts

| Part | For | Get it |
|---|---|---|
| **ACF for AI tools** (Windows, Linux, macOS) | Claude Code, Codex, WorkBuddy: your messages, what is handed to subtasks, what the AI reads, outgoing commands | **[0.4.0-beta.3](../../releases/tag/v0.4.0-beta.3)**, see below for each system |
| **ACF browser extension** | AI websites: claude.ai, ChatGPT, DeepSeek, Gemini: the message you send and the text files you upload | [Chrome Web Store](https://chromewebstore.google.com/detail/pjghhjaabjmjfbnllcgnidmfpgecgfbk) (also installable in Edge) |

> **Beta.** 0.4.0-beta.3 is an early test version. It is for friends who are willing to test it and send feedback, not as your only protection. Read the release notes and known limitations on the [release page](../../releases/tag/v0.4.0-beta.3) before installing.

## Get it for your system

All three are on the [0.4.0-beta.3 release page](../../releases/tag/v0.4.0-beta.3).

**Windows 10 / 11.** Download `ACF-Setup.exe` and run it. If an older ACF is installed, uninstall it first. It has no Microsoft code signature yet, so Windows and antivirus software may warn you. ACF and its rule packs update by themselves.

**Linux (Debian/Ubuntu-family desktops).** Download the `acf` and `acf-panel-runtime` `.deb` packages, their `.asc` signatures, `verify_deb_gpgv.sh` and `acf-linux-deb-release-keyring.gpg`. Check each package with `./verify_deb_gpgv.sh PACKAGE.deb PACKAGE.deb.asc`, then install both with `sudo apt install ./acf-panel-runtime_*.deb ./acf_*.deb`. Open the control panel with `acf panel` in a terminal. To update, install a new package.

The packages are signed with our Linux OpenPGP release key:

- Primary key: `C66A95EDE3C9A2ECF569D43216B5E948DEDC6180`
- Signing subkey: `A72107565CE6F382964F9EAEB52235D40CC4CD23`

**macOS 13 or later (Apple chip or Intel; tested on an Apple chip only).** Download the signed `.pkg`, open it and enter your administrator password. Open the control panel with `acf panel` in a terminal. To update, run `acf uninstall`, then open the new package.

## What happens when ACF finds something

- **Blocked:** keys, private keys and similar secrets are not sent; the AI tool's conversation (or the page) says why.
- **Asks you first:** for things such as card numbers, on Windows ACF shows its own confirmation window; only your click lets it through. On Linux and macOS that window isn't built yet: Claude Code asks in its own dialog before a tool runs, and everything else is blocked.
- **What ACF can't see** (desktop chat apps, AI agents running in a vendor's cloud, images and PDFs) is listed honestly in the known limitations and the Control Panel.

## Feedback

Email agent.context.firewall@gmail.com. In the Control Panel, "Pack logs to send us" creates a file you can attach; it holds ACF's check records only, never your conversations or file contents.

Privacy policy: [read it](https://vincentwang2014.github.io/acf-privacy/).

## Older downloads

The `v0.1.x-dev` releases are early development previews of the browser extension, kept for reference. Please use the Chrome Web Store version instead.
