# OpenClaw 新手完全指南

> 从零开始，手把手教你部署属于自己的 24 小时在线 AI 助手

![OpenClaw](https://img.shields.io/badge/OpenClaw-190K%2B%20Stars-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![更新时间](https://img.shields.io/badge/更新时间-2026年2月-orange)

## 📖 项目简介

OpenClaw（原名 Clawdbot、Moltbot）是一个开源的个人 AI 助手平台，在短短 3 周内突破 190,000+ Stars，成为 GitHub 历史上增长最快的开源项目之一。

**核心特性：**
- 🤖 真正的 AI Agent —— 不只是聊天，还能执行操作
- 🔒 本地运行 —— 数据完全由你掌控
- 🌐 多平台对接 —— 支持飞书、钉钉、微信、Telegram 等
- ⚡ 24小时在线 —— 云服务器部署全天候待命
- 🛠️ 1700+ Skills —— 丰富的技能扩展库

## 🚀 快速开始

根据你的平台选择对应教程：

| 平台 | 难度 | 推荐指数 | 教程链接 |
|------|------|----------|----------|
| Windows | ⭐⭐ | ⭐⭐⭐⭐⭐ | [Windows 安装指南](docs/windows/windows-install-guide.md) |
| macOS | ⭐⭐ | ⭐⭐⭐⭐ | [macOS 安装指南](docs/macos/macos-install-guide.md) |
| Linux | ⭐ | ⭐⭐⭐ | [Linux 安装指南](docs/linux/linux-install-guide.md) |
| 云服务器 | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | [云服务器部署指南](docs/cloud/cloud-deployment-guide.md) |
| Android | ⭐⭐⭐⭐ | ⭐⭐⭐ | [Android 部署指南](docs/android/android-deployment-guide.md) |

## 💰 API 平台推荐

OpenClaw 需要接入大模型 API 才能运行。以下是各平台的优惠信息：

| 平台                                                     | 新用户福利               | 邀请奖励      | 推荐指数  |
| ------------------------------------------------------ | ------------------- | --------- | ----- |
| [硅基流动](https://cloud.siliconflow.cn)                   | 注册送 2000万 Tokens    | 邀请双方各得代金券 | ⭐⭐⭐⭐⭐ |
| [阿里百炼](https://bailian.console.aliyun.com)             | 新人免费额度              | 每邀请1人得30元 | ⭐⭐⭐⭐⭐ |
| [火山方舟](https://www.volcengine.com/activity/codingplan) | Coding Plan 首月8.91元 | 邀请返利      | ⭐⭐⭐⭐  |
| [智谱 GLM](https://z.ai/subscribe)                       | Coding Plan 多档可选    | 最高40%返利   | ⭐⭐⭐⭐  |
| [MiniMax](https://www.minimaxi.com)                    | 新用户优惠               | 邀请者10%返利  | ⭐⭐⭐   |


👉 [查看详细 API 配置教程](docs/api-config/api-configuration.md)

## ☁️ 云服务器推荐

想要 24 小时在线的 AI 助手？推荐使用云服务器部署：

| 云服务商 | 套餐价格 | OpenClaw 支持 | 推荐指数 |
|----------|----------|---------------|----------|
| [阿里云轻量服务器](https://www.aliyun.com/product/swas) | 79元/年起 | 一键镜像部署 | ⭐⭐⭐⭐⭐ |
| [腾讯云轻量服务器](https://cloud.tencent.com/product/lighthouse) | 优惠套餐 | 官方教程支持 | ⭐⭐⭐⭐ |
| [百度智能云](https://cloud.baidu.com) | 多种套餐 | 一键部署教程 | ⭐⭐⭐ |

👉 [查看云服务器部署教程](docs/cloud/cloud-deployment-guide.md)

## 📱 平台对接

OpenClaw 支持对接多种消息平台：

| 平台 | 对接难度 | 教程链接 |
|------|----------|----------|
| 飞书 | ⭐⭐ | [飞书对接教程](docs/platform-integration/feishu-integration.md) |
| 钉钉 | ⭐⭐ | [钉钉对接教程](docs/platform-integration/dingtalk-integration.md) |
| Telegram | ⭐ | [Telegram对接教程](docs/platform-integration/telegram-integration.md) |
| 微信 | ⭐⭐⭐ | [微信对接教程](docs/platform-integration/wechat-integration.md) |

## 📚 目录结构

```
openclaw-tutorial/
├── README.md                    # 项目首页（本文件）
├── docs/                        # 教程文档目录
│   ├── windows/                 # Windows 相关教程
│   │   └── windows-install-guide.md
│   ├── macos/                   # macOS 相关教程
│   │   └── macos-install-guide.md
│   ├── linux/                   # Linux 相关教程
│   │   └── linux-install-guide.md
│   ├── cloud/                   # 云服务器相关教程
│   │   └── cloud-deployment-guide.md
│   ├── android/                 # Android 相关教程
│   │   └── android-deployment-guide.md
│   ├── api-config/              # API 配置教程
│   │   └── api-configuration.md
│   └── platform-integration/    # 平台对接教程
│       ├── platform-integration-overview.md
│       ├── feishu-integration.md
│       ├── dingtalk-integration.md
│       ├── telegram-integration.md
│       └── wechat-integration.md
├── scripts/                     # 一键脚本
│   ├── install-windows.bat
│   ├── install-linux.sh
│   └── check-env.sh
├── images/                      # 教程图片
└── templates/                   # 配置模板
    ├── config-template.json
    └── env-template.txt
```

## ❓ 常见问题

<details>
<summary><b>Q: OpenClaw 和 ChatGPT 有什么区别？</b></summary>

OpenClaw 不是简单的聊天机器人，而是一个可以真正"动手"的 AI Agent。它能够：
- 执行终端命令
- 操作文件系统
- 控制浏览器
- 发送邮件、管理日历
- 对接各种消息平台

这使得它能够完成复杂的多步骤任务，而不仅仅是回答问题。
</details>

<details>
<summary><b>Q: 哪个 API 平台最推荐？</b></summary>

推荐根据你的需求选择：
- **新手入门**：硅基流动（免费额度多，上手简单）
- **性价比优先**：火山方舟 Coding Plan（首月仅8.91元）
- **长期使用**：智谱 GLM Coding Plan（年付优惠力度大）
- **阿里生态用户**：阿里百炼（与阿里云整合好）
</details>

<details>
<summary><b>Q: 云服务器配置要求是什么？</b></summary>

最低配置：
- CPU: 1核
- 内存: 1GB
- 存储: 20GB
- 系统: Ubuntu 20.04+ / CentOS 7+

推荐配置：
- CPU: 2核
- 内存: 2GB
- 存储: 40GB
- 系统: Ubuntu 22.04

阿里云 79元/年的轻量应用服务器完全满足需求。
</details>

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request 帮助完善教程！

## 📄 许可证

本项目采用 MIT 许可证。

---

**⭐ 如果这个教程对你有帮助，请给个 Star 支持一下！**

---

*本教程包含推荐链接，通过链接注册可享受额外优惠，同时也支持作者持续产出优质内容。*
