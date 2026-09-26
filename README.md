# Mosyn plugin

Mosyn is an Android study app. Hand your assistant a list, a reading, or a call sheet, and the study
set it implies builds itself on your phone, with a verified picture for every entry. The assistant
can also write a custom study game for the set.

This repository is the Mosyn plugin for Claude Code, Claude, and Codex, and the marketplace that
serves it. The plugin adds the Mosyn connector (`https://mosyn.lycatra.com/mcp`) and a skill that
teaches the assistant how to build a good set.

## Before you start

Install Mosyn on your Android phone and sign in: [mosyn.lycatra.com/download](https://mosyn.lycatra.com/download).
The connection is approved inside that app.

## Install

Claude Code:

```sh
claude plugin marketplace add Lycatra/mosyn
claude plugin install mosyn@mosyn --scope user
```

Codex:

```sh
codex plugin marketplace add Lycatra/mosyn
codex plugin add mosyn@mosyn
```

Claude (web and desktop): Customize → Plugins → add the marketplace `Lycatra/mosyn`, then install
Mosyn. To add only the connector, use Customize → Connectors → Add custom connector with the URL
`https://mosyn.lycatra.com/mcp`.

Other assistants and editors, and agents setting this up on their own: [mosyn.lycatra.com/connect](https://mosyn.lycatra.com/connect)
and [mosyn.lycatra.com/agents.md](https://mosyn.lycatra.com/agents.md).

## Approve the connection

The first time the assistant uses Mosyn, a page on mosyn.lycatra.com opens with an 8-character
code and a QR code. Scan the QR with your phone, or open Mosyn → Settings → Connect an assistant
and type the code, then approve. The page finishes by itself. Requests expire after 10 minutes.

Check it worked by asking: *What study sets do I have in Mosyn?*

## Links

- Website: [mosyn.lycatra.com](https://mosyn.lycatra.com)
- Privacy: [mosyn.lycatra.com/privacy](https://mosyn.lycatra.com/privacy)
- Terms: [mosyn.lycatra.com/terms](https://mosyn.lycatra.com/terms)
- Support: [mosyn@lycatra.com](mailto:mosyn@lycatra.com)
