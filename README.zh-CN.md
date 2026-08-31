# DeepSeek Harness Channels

这是面向 [DeepSeek Harness](https://github.com/mapan0424/deepseek-harness) 的社区插件集合。

当前仓库包含四个包：

- `@anarkhgatsby/deepseek-harness-core`：共享消息总线与 Gateway 核心。
- `@anarkhgatsby/deepseek-harness-channel-config`：可视化渠道配置界面。
- `@anarkhgatsby/deepseek-harness-channel-feishu`：飞书 / Lark 渠道插件。
- `@anarkhgatsby/deepseek-harness-channel-imessage`：仅本机的 macOS iMessage 插件，通过 Messages.app 和 chat.db 工作。

## 安装

将以下插件安装到 `web` profile：

```bash
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-core
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-imessage
```

其中 `core` 是共享依赖，`config` 提供可视化配置页面，`feishu` 提供飞书渠道，`imessage` 提供 macOS 本机 iMessage 渠道。iMessage 插件不使用 `imsg` CLI、Photon 或任何云中继。

## iMessage 配置

1. 在 macOS 上登录 Messages.app 的 iMessage。
2. 为 DeepSeek Harness 开启“完全磁盘访问”，使其可以读取 `~/Library/Messages/chat.db`。
3. 在“自动化”设置中允许 DeepSeek Harness 控制“信息”应用。
4. 安装 iMessage 插件，在渠道配置页确认数据库路径和工作空间路径。
5. 向配置的账号发送消息，验证本地监听和回复链路。

入站消息从本机数据库读取，出站消息通过 AppleScript 控制 Messages.app 发送，消息内容不会经过第三方云服务。

## 飞书配置

1. 创建飞书 / Lark 应用，并开启机器人所需权限。
2. 在 DeepSeek Harness 的渠道配置页面填写 App ID 和 App Secret。
3. 启用飞书渠道并保存配置。
4. 给机器人发送消息，验证收发是否正常。

飞书插件使用长连接模式。默认状态文件保存在当前系统用户的 `.dsh` 目录下，路径会根据操作系统用户目录动态解析，不会写死为作者电脑的路径。

## 兼容性

当前版本面向 DeepSeek Harness / DSH `0.1.1-rc.2` 包版本线和 Cordis 4.x，适用于桌面端的 `web` profile。iMessage 插件仅支持 macOS，并需要上述系统隐私权限。

## 验证状态

- Core：已完成打包，并作为共享运行时依赖进行冒烟测试。
- 可视化配置：已在桌面端加载验证；iMessage 配置仅暴露本机模式。
- 飞书：已在桌面端本地验证；实际连接需要填入有效的飞书凭据。
- iMessage：已完成本地 adapter 语法检查，并在桌面运行时包中验证；实际使用需要 macOS 隐私权限。

## 许可证

MIT，详见 [LICENSE](LICENSE)。
