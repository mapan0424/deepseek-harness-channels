# DeepSeek Harness Channels

中文文档：[README.zh-CN.md](README.zh-CN.md)

Official and community channel integration packages for [DeepSeek Harness (DSH)](https://github.com/mapan0424/deepseek-harness).

Connect external messaging platforms (Feishu/Lark, WeCom, iMessage, etc.) directly to your local DeepSeek AI agents through a unified, zero-relay message bus architecture.

---

## 📦 Package Matrix

| Package Name | npm Version | Type | Description |
| :--- | :---: | :---: | :--- |
| **`@anarkhgatsby/deepseek-harness-core`** | `0.1.0` | Core Library | Unified message bus, session lifecycle, workspace routing, deduplication, and serial queuing |
| **`@anarkhgatsby/deepseek-harness-channel-config`** | `0.1.4` | Visual Console | Settings UI for channel management, official Squircle brand assets, Dark Mode adaptive, and parameter configuration |
| **`@anarkhgatsby/deepseek-harness-channel-feishu`** | `0.1.0` | Channel Adapter | Feishu / Lark AI Bot channel (Official WebSocket outbound long-connection mode) |
| **`@anarkhgatsby/deepseek-harness-channel-wecom`** | `0.1.1` | Channel Adapter | WeCom (企业微信) AI Bot channel (Official WebSocket long-connection stack) |
| **`@anarkhgatsby/deepseek-harness-channel-imessage`** | `0.1.1` | Channel Adapter | macOS local-only iMessage channel (Local `chat.db` listener + AppleScript outbound) |

---

## ⚡ Quick Install

Install the desired packages into your DeepSeek Harness `web` profile:

```bash
# 1. Install core message bus and visual config console (Required)
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-core
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-config

# 2. Install channel adapters as needed
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-wecom
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-imessage
```

> **Note**: Restart DeepSeek Harness after installation to view all channels under **Settings ➔ Channels**.

---

## 📖 Channel Setup Guides

### 1. 🕊️ Feishu / Lark Setup

The Feishu channel uses **official outbound WebSocket long-connection mode**. No public IP, webhook URL, or reverse proxy is required.

1. Open the [Feishu Open Platform Console](https://open.feishu.cn/app) and create an enterprise custom app.
2. Under **Add Capabilities**, add the **Bot** capability.
3. Under **Permissions**, grant:
   - `im:message`, `im:message:send_as_bot`
   - `im:message.group_at_msg:readonly`, `im:message.p2p_msg:readonly`
4. Under **Events and Callbacks ➔ Event Configuration**, select **"Use long connection to receive events"** and add `im.message.receive_v1`.
5. Create and publish an app version.
6. Copy `App ID` and `App Secret` from **Credentials & Basic Info**, paste them into DeepSeek Harness channel settings, and toggle the channel on.

---

### 2. 💬 WeCom (企业微信) Setup

The WeCom channel connects directly to Tencent's cloud WebSocket gateway (`wss://openws.work.weixin.qq.com`).

1. Log in to the [WeCom Admin Console](https://work.weixin.qq.com/).
2. Navigate to **App Management ➔ AI Bot / Custom Apps** and create an AI Bot.
3. Retrieve your `botId` and `secret`.
4. In DeepSeek Harness **Settings ➔ Channels**, configure `botId`, `secret`, and the target workspace, then toggle the channel on.

---

### 3. 🍏 iMessage Setup (macOS only)

The iMessage channel operates completely locally. Inbound messages are read from `~/Library/Messages/chat.db` and outbound messages are sent via native AppleScript. **No message content ever touches a third-party cloud service.**

1. Ensure macOS Messages.app is signed in with your Apple ID.
2. Go to **macOS System Settings ➔ Privacy & Security**:
   - Grant **Full Disk Access** to DeepSeek Harness.
   - Grant **Automation** permission for DeepSeek Harness to control Messages.app.
3. Open DeepSeek Harness Settings ➔ Channels and enable iMessage.

---

## 🔒 Privacy & Security

- **Zero Cloud Relays**: All connections are point-to-point (direct to official WebSocket gateways or local database).
- **Local Credentials**: API secrets are stored locally in `~/.dsh/settings.yaml` with strict filesystem permissions.
- **Session Isolation**: Each external user/chat is routed to an isolated session space with configurable workspace roots.

---

## 📄 License

MIT. See [LICENSE](LICENSE).
