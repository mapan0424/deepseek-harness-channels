# DeepSeek Harness Channels

中文文档：[README.zh-CN.md](README.zh-CN.md)

Community channel packages for [DeepSeek Harness](https://github.com/mapan0424/deepseek-harness).

This repository currently contains four packages:

- `@anarkhgatsby/deepseek-harness-core` — shared message bus and gateway core.
- `@anarkhgatsby/deepseek-harness-channel-config` — visual channel configuration UI.
- `@anarkhgatsby/deepseek-harness-channel-feishu` — Feishu/Lark channel integration.
- `@anarkhgatsby/deepseek-harness-channel-imessage` — local-only macOS iMessage integration through Messages.app and chat.db.

## Install

Install the packages into the `web` profile:

```bash
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-core
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-imessage
```

The `core` package is a shared dependency. The config package adds the visual configuration page. The Feishu package adds Feishu/Lark. The iMessage package is macOS-only and uses the local Messages database and Messages.app; it does not use the `imsg` CLI, Photon, or a cloud relay.

## iMessage setup

1. Use macOS with Messages.app signed in to iMessage.
2. Grant DeepSeek Harness Full Disk Access so it can read `~/Library/Messages/chat.db`.
3. Grant Automation permission for DeepSeek Harness to control Messages.app.
4. Install the iMessage package and configure the database path and workspace in the channel configuration page.
5. Send a message to the configured account to verify the local listener and reply path.

Messages are read from the local database and sent through Messages.app using AppleScript. No message content is sent through a third-party cloud service.

## Feishu setup

1. Create a Feishu/Lark app and enable the required bot permissions.
2. Copy the App ID and App Secret into the DeepSeek Harness channel configuration page.
3. Enable the Feishu channel and save the configuration.
4. Start a chat with the bot to verify message delivery.

The Feishu adapter uses the long connection mode and stores its local gateway state under the current user's `.dsh` directory by default. Paths are resolved from the operating system user home directory; they are not tied to the author's Mac account.

## Compatibility

These packages target the DeepSeek Harness / DSH `0.1.1-rc.2` package line and Cordis 4.x. The iMessage package requires macOS and the Messages.app authorization described above.

## Verification status

- Core: packaged and smoke-tested as the shared runtime dependency.
- Visual config: packaged and loaded in the desktop app; iMessage configuration exposes only the local mode.
- Feishu: tested locally with the desktop app; valid Feishu credentials are required for a live connection.
- iMessage: local adapter syntax-checked and verified in the desktop runtime bundle; live use requires macOS privacy permissions.

## License

MIT. See [LICENSE](LICENSE).
