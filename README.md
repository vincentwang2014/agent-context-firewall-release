# Agent Context Firewall (browser extension, development preview)

[中文](README.zh-CN.md)

Checks what you are about to send to an AI, on your own computer, before it is sent: keys and private keys are stopped; personal information such as social security or card numbers is sent only after you confirm.

> **Development preview.** For feedback, not as your only protection.

## What it does

Supported sites: **claude.ai** and **ChatGPT** (chatgpt.com).

When you press send, the extension checks the message first:

| Found | What happens |
|---|---|
| Private keys, API tokens, AWS access keys | **Blocked.** No override; change the content and send again |
| Card numbers, US bank routing numbers, US Social Security numbers | **Asks you first.** Confirming sends it this once only |
| Uploaded text files | Checked the same way |
| Files whose content can't be checked (images, PDFs, ...) | Asks whether to send them unchecked |
| The extension itself fails | **Nothing is sent**, to be safe |

The toolbar shield: **green** = protection is on; **red** = protection is unavailable and nothing is sent; **grey** = starting.

## Your data

- **All checking happens on your computer.** In this version the extension sends nothing anywhere; it only reads files inside its own package.
- It keeps on this device only: the **time, site, result and category** of the last 10 events (for example "Blocked (credentials)"), and your chosen usage style. **Message content is never stored.**
- Confirmations live in the browser session and are cleared when the browser closes.
- Removing the extension removes all of the above.

## Install

Desktop Chrome. Edge and other Chromium-based browsers usually work too: turn on developer mode on their extensions page and load the unpacked folder; the menu names differ slightly.

1. Download the latest `acf-browser-….zip` from [Releases](../../releases).
2. (Optional) Check it: the zip's SHA-256 must equal the last line of the `.SHA256SUMS` file in the same release.
   Windows: `certutil -hashfile acf-browser-….zip SHA256`; macOS / Linux: `shasum -a 256 acf-browser-….zip`
3. Unzip it.
4. Open `chrome://extensions` and turn on **Developer mode** (top right).
5. Click **Load unpacked** and choose the unzipped folder (the one containing `manifest.json`).
6. Refresh any claude.ai / ChatGPT tabs already open.
7. Pin the shield via the puzzle-piece icon and check it is green.

**Remove:** click **Remove** in `chrome://extensions`.

## Known limits

- **Development signing:** the rule packs are signed with public development keys. That detects corruption, not deliberate tampering. A release build will use publisher keys.
- **False positives are possible**, e.g. some 9-digit numbers may look like an SSN.
- **Only the two sites above**, and only messages sent from the web page. A site redesign can leave some way of sending unchecked for a while (the extension tries to say "couldn't confirm it was checked").
- The usage styles (Quiet / Standard / Strict) behave the same with today's rules.
- The UI follows Chrome's display language (English or Chinese).
- **Other extensions are not watched.** This extension checks what these two sites send to the AI service. It can't see or stop another browser extension that reads the page and sends data out from its own background -- Chrome doesn't let one extension see another's network requests. That is the job of your anti-malware software and of installing only extensions you trust (in a company, usually an extension allowlist).

## Feedback

Please tell us about:

- **False positives:** something blocked that shouldn't be -- what kind of content (please don't send the real sensitive data itself) and which site;
- **Misses:** something that should have been stopped and wasn't;
- **The UI:** anything unclear or awkward;
- the version: `commit` in `BUILD_INFO.json` in the unzipped folder.

How to send feedback: contact the person who sent you this link.
