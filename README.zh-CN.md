# DeepSeek Harness Channels

这是面向 [DeepSeek Harness](https://github.com/mapan0424/deepseek-harness) 的社区插件集合。

当前仓库包含三个包：

- `@anarkhgatsby/deepseek-harness-core`：共享消息总线与 Gateway 核心。
- `@anarkhgatsby/deepseek-harness-channel-config`：可视化渠道配置界面。
- `@anarkhgatsby/deepseek-harness-channel-feishu`：飞书 / Lark 渠道插件。

## 安装

将以下插件安装到 `web` profile：

```bash
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-core
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-feishu
```

其中 `core` 是共享依赖；`config` 提供可视化配置页面；`feishu` 提供飞书渠道，安装后可以在配置页面中设置。

## 飞书配置

1. 创建飞书 / Lark 应用，并开启机器人所需权限。
2. 在 DeepSeek Harness 的渠道配置页面填写 App ID 和 App Secret。
3. 启用飞书渠道并保存配置。
4. 给机器人发送消息，验证收发是否正常。

飞书插件使用长连接模式。默认状态文件保存在当前系统用户的 `.dsh` 目录下，路径会根据操作系统用户目录动态解析，不会写死为作者电脑的路径。

## 兼容性

当前版本面向 DeepSeek Harness / DSH `0.1.1-rc.2` 包版本线和 Cordis 4.x，适用于桌面端的 `web` profile。

## 验证状态

- Core：已完成打包，并作为共享运行时依赖进行冒烟测试。
- 可视化配置：已在桌面端加载验证。
- 飞书：已在桌面端本地验证；实际连接需要填入有效的飞书凭据。

其他渠道插件暂时不放入本仓库，待分别验证后再发布。

## 许可证

MIT，详见 [LICENSE](LICENSE)。
