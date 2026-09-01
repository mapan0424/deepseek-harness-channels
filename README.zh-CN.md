# DeepSeek Harness Channels

English documentation: [README.md](README.md)

面向 [DeepSeek Harness (DSH)](https://github.com/mapan0424/deepseek-harness) 的官方与社区通道（Channel）扩展包集合。

通过统一的消息总线架构，将外部即时通讯工具（飞书、企业微信、iMessage 等）与本地 DeepSeek 核心 Agent 无缝串联，实现随时随地通过手机/桌面聊天软件调用本地 AI 进行多轮对话、自动化工具调用与知识库问答。

---

## 📦 插件包矩阵

| 插件名称 | npm 版本 | 类型 | 说明 |
| :--- | :---: | :---: | :--- |
| **`@anarkhgatsby/deepseek-harness-core`** | `0.1.0` | 核心共享库 | 统一消息总线、会话生命周期管理、工作空间映射、去重与并发串行队列 |
| **`@anarkhgatsby/deepseek-harness-channel-config`** | `0.1.4` | 可视化控制台 | 设置页「消息通道」面板，提供官方满格图标、暗黑模式适配、图形化启停与参数配置 |
| **`@anarkhgatsby/deepseek-harness-channel-feishu`** | `0.1.0` | 通道适配器 | 飞书 / Lark 开放平台智能机器人（官方 WebSocket 出站长连接模式） |
| **`@anarkhgatsby/deepseek-harness-channel-wecom`** | `0.1.1` | 通道适配器 | 企业微信 AI 智能机器人（腾讯官方 WebSocket 长连接协议栈） |
| **`@anarkhgatsby/deepseek-harness-channel-imessage`** | `0.1.1` | 通道适配器 | macOS 本机 iMessage 直连（本地 `chat.db` 监听 + AppleScript 出站） |

---

## ⚡ 快速安装

将通道插件安装至 DeepSeek Harness 的 `web` profile：

```bash
# 1. 安装核心总线与可视化控制台（必须）
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-core
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-config

# 2. 根据需要安装通道插件（可多选）
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-wecom
dsh plugin --profile web add @anarkhgatsby/deepseek-harness-channel-imessage
```

> **提示**：安装完成后重启客户端，即可在客户端 **「设置 ➔ 消息通道」** 页面看到已接入的渠道。

---

## 📖 渠道配置与接入指南

### 1. 🕊️ 飞书 / Lark 机器人配置

飞书通道采用**官方 WebSocket 出站长连接模式**，无需配置公网 IP、域名或反向代理，在本地内网即可稳定接收推送与回复。

#### 第一步：创建飞书开放平台应用
1. 打开 [飞书开放平台控制台](https://open.feishu.cn/app) 并登录；
2. 点击 **「创建企业自建应用」**，填写应用名称与图标；
3. 进入应用详情页，在 **「添加应用能力」** 中添加 **「机器人」**。

#### 第二步：配置权限范围
在左侧菜单 **「权限管理」** 中，开通以下权限：
- `获取与发送单聊、群组消息`（`im:message`、`im:message:send_as_bot`）
- `以应用的身份发消息`（`im:message.group_at_msg:readonly`、`im:message.p2p_msg:readonly`）

#### 第三步：开启事件长连接与发布版本
1. 进入左侧 **「事件与回调 ➔ 事件配置」**；
2. 订阅方式选择 **「使用长连接接收事件」**（无需填写请求网址）；
3. 添加事件：`接收消息 v2.0`（`im.message.receive_v1`）；
4. 进入 **「版本管理与发布」**，创建并发布一个新版本，企业管理员审批通过后生效。

#### 第四步：填入 DeepSeek Harness 并开启
1. 在飞书后台 **「凭证与基础信息」** 复制 `App ID` 和 `App Secret`；
2. 打开 DeepSeek Harness 客户端，进入 **「设置 ➔ 消息通道」**；
3. 点击飞书右侧的 **「⚙️ 配置参数」** 按钮，填入 `App ID` 与 `App Secret`；
4. 开启右侧开关并保存。在飞书里直接向机器人发消息测试多轮对话！

---

### 2. 💬 企业微信 (WeCom) 机器人配置

企业微信通道基于官方智能机器人长连接协议（`wss://openws.work.weixin.qq.com`），直连腾讯云端网关，安全稳定。

#### 第一步：获取企业微信智能机器人凭据
1. 登录 [企业微信管理后台](https://work.weixin.qq.com/)；
2. 进入 **「应用管理 ➔ 智能机器人 / 自建应用」** 创建一个机器人；
3. 在机器人详情页获取专属的 **`botId`** 与 **`secret`**。

#### 第二步：填入 DeepSeek Harness 并开启
1. 打开 DeepSeek Harness 客户端，进入 **「设置 ➔ 消息通道」**；
2. 点击企业微信右侧的 **「⚙️ 配置参数」** 按钮；
3. 填入 `botId` 和 `secret`，选择默认绑定的本地工作空间（Workspace）；
4. 开启通道开关并保存。企微成员在单聊或群聊 @机器人 发送消息即可自动回复！

---

### 3. 🍏 iMessage 本机直连配置 (macOS 专属)

iMessage 通道为纯本地安全运行架构，入站直接读取本机 `chat.db`，出站通过 macOS 原生 AppleScript 控制信息应用发送。**消息全程在本地闭环，绝不经过任何第三方云服务。**

#### 第一步：登录 macOS 信息应用
确保 macOS 系统的「信息」（Messages.app）已登录你的 Apple ID，且能正常收发 iMessage。

#### 第二步：授予 macOS 系统隐私权限
1. 打开 macOS **「系统设置 ➔ 隐私与安全性」**；
2. 进入 **「完全磁盘访问权限」**，勾选并允许 **DeepSeek Harness**（允许读取 `~/Library/Messages/chat.db`）；
3. 进入 **「自动化」**，确保 DeepSeek Harness 拥有控制 **「信息 (Messages)」** 的权限。

#### 第三步：开启 iMessage 通道
1. 打开 DeepSeek Harness 进入 **「设置 ➔ 消息通道」**；
2. 确认权限状态提示正常，开启右侧开关即可。

---

## 🎨 可视化控制台特性 (`channel-config`)

- **官方品牌视觉标准**：全通道 100% 满格原版 Squircle 资产，精确适配 macOS 视觉规范；
- **全场景暗黑模式自适应**：支持系统深浅色与 DSH 内部主题切换（`body[data-ds-dark-theme]`），高反差配色，杜绝融底与杂色；
- **极简专业 UI**：全量内置 DSH 官方矢量图标库（`@deepseek-ai/dsh-client-ui-primitives`），告别 Emoji 渲染不一致；
- **实时运行监控**：支持流光状态指示灯、活跃会话统计、通道密码明文/密文切换与热重载。

---

## 🔒 隐私与安全性

1. **零中间服务器**：所有通道均为本地直连官方长连接网关（飞书/企微）或本机数据库（iMessage），没有中继跳板；
2. **凭据安全**：所有密钥本地加密保存在用户目录的 `~/.dsh/settings.yaml` 中，不上传云端；
3. **独立会话隔离**：每个通道用户在本地分配独立 Session 空间，支持为不同联系人定制不同的工作区（Workspace）与工具权限。

---

## 🛠️ 兼容性说明

- **平台**：macOS (Intel / Apple Silicon)、Linux、Windows（iMessage 仅限 macOS）
- **DeepSeek Harness 运行时**：DSH `0.1.1-rc.2` / Cordis 4.x
- **Node.js**：Node >= 18.0.0 (推荐 Node 20 / 22)

---

## 📄 许可证

本项目采用 [MIT 许可证](LICENSE) 开源。
