# DeepSeek Harness Channels

中文文档：[README.zh-CN.md](README.zh-CN.md)

Community channel packages for [DeepSeek Harness](https://github.com/mapan0424/deepseek-harness).

This repository currently contains three packages:

- `@anarkhgatsby/deepseek-harness-core` — shared message bus and gateway core.
- `@anarkhgatsby/deepseek-harness-channel-config` — visual channel configuration UI.
- `@anarkhgatsby/deepseek-harness-channel-feishu` — Feishu/Lark channel integration.

## Install

Install the packages into the `web` profile:

```bash
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-core
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-feishu
```

The `core` package is a shared dependency. The config package adds the visual configuration page. The Feishu package adds the Feishu channel and is configured from that page.

## Feishu setup

1. Create a Feishu/Lark app and enable the required bot permissions.
2. Copy the App ID and App Secret into the DeepSeek Harness channel configuration page.
3. Enable the Feishu channel and save the configuration.
4. Start a chat with the bot to verify message delivery.

The Feishu adapter uses the long connection mode and stores its local gateway state under the current user's `.dsh` directory by default. Paths are resolved from the operating system user home directory; they are not tied to the author's Mac account.

## Compatibility

These packages target the DeepSeek Harness / DSH `0.1.1-rc.2` package line and Cordis 4.x. They are intended for the desktop app and web profile.

## Verification status

- Core: packaged and smoke-tested as the shared runtime dependency.
- Visual config: packaged and loaded in the desktop app.
- Feishu: tested locally with the desktop app; valid Feishu credentials are required for a live connection.

Other channel adapters are intentionally not included in this repository yet.

## License

MIT. See [LICENSE](LICENSE).
