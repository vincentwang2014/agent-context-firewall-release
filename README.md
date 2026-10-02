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
| Files whose content can't be checked (images, PDFs, ...) | Sent as usual, without a card; listed under Recent as "uploaded without checking" |
| The extension itself fails, or can't read what the site sends | Sent as usual, **without checking**; the shield turns amber and Recent lists it |

The rule: the extension stops or asks you only when it actually finds something. When it can't do its own job, your message goes out as if the extension weren't installed, and it says so honestly instead of interrupting you. If you prefer "hold anything that can't be checked", choose the **Strict** usage style in Settings: files that can't be checked are asked about first, and nothing is sent while protection isn't working.

It reads only what you send: the message you typed and the files you upload, at the site's own send and upload addresses. The site's other traffic (analytics, settings, your avatar) is left alone.

The toolbar shield: **green** = protection is on; **amber** = protection isn't working right now, messages are sent without checking (amber on a single tab: on that page, a message or a file you added didn't go out the way the extension recognises, so it can't confirm it was checked, or the page was open before the extension was installed or updated and needs a refresh -- the popup says which); **red** = the same in the Strict style, where nothing is sent; **grey** = starting.

> **Changed in v0.1.5-dev.** After an install or update, pages that were already open no longer get a notice drawn on them: their tab's shield turns amber and the popup asks you to refresh. The extension no longer asks for the permission to run scripts in pages. Updating from v0.1.4-dev, a page still open from before may show the old refresh notice one last time.
>
> **Changed in v0.1.4-dev.** Only your message and your files are read (before, other requests to the site were checked too, which caused the stray "unknown upload" cards on ChatGPT). The per-tab amber shield is new. Recent no longer lists every ordinary send.
>
> **Changed in v0.1.3-dev.** Before it, the extension asked before sending a file that can't be checked and sent nothing when it failed (red shield).

## Your data

- **All checking happens on your computer.** In this version the extension sends nothing anywhere; it only reads files inside its own package.
- It keeps on this device only: the **time, site, result and category** of the last 10 events (for example "Blocked (credentials)"; ordinary sends with nothing found are not listed), and your chosen usage style. **Message content is never stored.**
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
- **Only the two sites above**, and only messages sent from the web page. A site redesign can leave some way of sending unchecked for a while; when the extension notices, the popup says so for that tab.
- **While a site has changed its format, or the extension isn't working, messages go out unchecked** (except in Strict). You see it on the shield and in the popup, not on the page.
- The usage styles: a real finding is blocked or asked about the same way in all three; only Strict holds what the extension can't check.
- The UI follows Chrome's display language (English or Chinese).
- **Other extensions are not watched.** This extension checks what these two sites send to the AI service. It can't see or stop another browser extension that reads the page and sends data out from its own background -- Chrome doesn't let one extension see another's network requests. That is the job of your anti-malware software and of installing only extensions you trust (in a company, usually an extension allowlist).

## Feedback

Please tell us about:

- **False positives:** something blocked that shouldn't be -- what kind of content (please don't send the real sensitive data itself) and which site;
- **Misses:** something that should have been stopped and wasn't;
- **The UI:** anything unclear or awkward;
- the version: `commit` in `BUILD_INFO.json` in the unzipped folder.

How to send feedback: contact the person who sent you this link.
