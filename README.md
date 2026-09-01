# DeepSeek Harness Channels

中文文档：[README.zh-CN.md](README.zh-CN.md)

Channel packages for [DeepSeek Harness](https://github.com/mapan0424/deepseek-harness).

This repository contains:

- `@anarkhgatsby/deepseek-harness-core` — shared message bus and gateway core.
- `@anarkhgatsby/deepseek-harness-channel-config` — visual channel configuration UI (Feishu, WeCom, iMessage).
- `@anarkhgatsby/deepseek-harness-channel-feishu` — Feishu/Lark bot channel (WebSocket long-connection).
- `@anarkhgatsby/deepseek-harness-channel-wecom` — WeCom (企业微信) AI Bot channel (WebSocket long-connection).
- `@anarkhgatsby/deepseek-harness-channel-imessage` — macOS local iMessage channel.

## Install

Install the packages into the `web` profile:

```bash
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-core
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-wecom
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-imessage
```

## Configuration

Open the DeepSeek Harness Settings ➔ Channels tab to configure credentials and toggle channels interactively.

## License

MIT. See [LICENSE](LICENSE).
