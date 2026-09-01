# DeepSeek Harness Channels

English documentation: [README.md](README.md)

面向 [DeepSeek Harness](https://github.com/mapan0424/deepseek-harness) 的官方/社区通道插件集合。

当前仓库包含以下插件包：

- `@anarkhgatsby/deepseek-harness-core`：共享消息总线与网关核心。
- `@anarkhgatsby/deepseek-harness-channel-config`：可视化通道配置界面（支持企微、飞书、iMessage 官方原版图标与参数管理）。
- `@anarkhgatsby/deepseek-harness-channel-feishu`：飞书 / Lark 智能机器人通道（长连接模式）。
- `@anarkhgatsby/deepseek-harness-channel-wecom`：企业微信智能机器人通道（WebSocket 出站长连接）。
- `@anarkhgatsby/deepseek-harness-channel-imessage`：iMessage 本地通道（macOS 原生 chat.db 与 AppleScript 自动化）。

## 安装

将以下插件安装到 `web` profile：

```bash
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-core
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-wecom
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-imessage
```

其中 `core` 是共享依赖；`channel-config` 提供可视化配置页面；各通道安装后可直接在「设置 ➔ 消息通道」页面进行图形化启停与参数配置。

## 飞书配置

1. 创建飞书 / Lark 应用，并开启机器人所需权限。
2. 在 DeepSeek Harness 的消息通道配置页面填写 App ID 和 App Secret。
3. 启用飞书通道并保存配置。
4. 给机器人发送消息，验证收发与多轮对话。

## 企业微信配置

1. 在企业微信后台创建自建应用/智能机器人，获取 `botId` 和 `secret`。
2. 在 DeepSeek Harness 消息通道页面填入对应参数并开启通道。
3. 插件自动建立 WebSocket 安全出站长连接（无需公网 IP 与复杂回调配置）。

## iMessage 配置 (macOS)

1. 在「系统设置 ➔ 隐私与安全性」中为 DeepSeek Harness 开启「完全磁盘访问权限」及「自动化」。
2. 在通道页面开启 iMessage 即可实现本地端到端收发。

## 兼容性

当前版本面向 DeepSeek Harness / DSH `0.1.1-rc.2` 包版本线和 Cordis 4.x，适用于桌面端与 web profile。

## 许可证

MIT，详见 [LICENSE](LICENSE)。
