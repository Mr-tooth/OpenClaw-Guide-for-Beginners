# QQBot 集成指南

**创建时间**: 2026-05-01
**最后更新**: 2026-05-01
**适用版本**: OpenClaw v2026.4.27+

## 📖 概述

QQBot 是 OpenClaw v2026.4.27 新增的渠道支持，允许你通过 QQ 机器人与 OpenClaw 进行对话，支持群聊、流式响应和媒体上传。

## 🎯 核心功能

### 主要特性
- **群聊支持**: 支持 QQ 群聊对话
- **流式响应**: 支持实时流式消息
- **媒体上传**: 支持图片、视频、语音上传
- **C2C 消息**: 支持点对点消息
- **管道重构**: 优化消息处理流程

### 支持的功能
- **文本对话**: 支持文本消息收发
- **媒体消息**: 支持图片、视频、语音消息
- **表情反应**: 支持表情反应
- **群聊管理**: 支持群聊权限管理

## 🔧 配置步骤

### 步骤1: 创建 QQ 机器人

1. 访问 [QQ 开放平台](https://q.qq.com)
2. 登录账号并进入控制台
3. 点击"创建机器人"
4. 填写机器人信息：
   - 机器人名称：OpenClaw Assistant
   - 机器人描述：AI 助手机器人
   - 机器人头像：上传头像图片
5. 选择机器人类型：
   - 群聊机器人
   - 私聊机器人
6. 点击"创建"完成机器人创建

### 步骤2: 获取 API 凭证

1. 进入机器人设置页面
2. 找到"API 凭证"部分
3. 复制以下信息：
   - App ID
   - App Secret
   - Token
   - EncodingAESKey

### 步骤3: 配置 OpenClaw

#### 方法1: 使用命令行

```bash
# 启用 QQBot 渠道
openclaw config set channels.qqbot.enabled true

# 设置 App ID
openclaw config set channels.qqbot.appId "your-app-id"

# 设置 App Secret
openclaw config set channels.qqbot.appSecret "your-app-secret"

# 设置 Token
openclaw config set channels.qqbot.token "your-token"

# 设置 EncodingAESKey
openclaw config set channels.qqbot.encodingAESKey "your-encoding-aes-key"

# 验证配置
openclaw config get channels.qqbot
```

#### 方法2: 使用配置文件

在 `~/.openclaw/openclaw.json` 中添加：

```json
{
  "channels": {
    "qqbot": {
      "enabled": true,
      "appId": "your-app-id",
      "appSecret": "your-app-secret",
      "token": "your-token",
      "encodingAESKey": "your-encoding-aes-key",
      "webhookUrl": "https://your-server.com/webhook/qqbot",
      "autoReply": true,
      "messageTimeout": 30000,
      "sandbox": false
    }
  }
}
```

### 步骤4: 配置 Webhook

1. 在 QQ 开放平台进入机器人设置
2. 找到"事件订阅"部分
3. 设置 Webhook URL：
   ```
   https://your-server.com/webhook/qqbot
   ```
4. 选择订阅的事件：
   - C2C 消息接收事件
   - 群聊消息接收事件
   - 成员列表事件
   - 文件上传事件

### 步骤5: 启动 OpenClaw

```bash
# 启动 Gateway
openclaw gateway start

# 查看渠道状态
openclaw channels status

# 测试 QQBot 渠道
openclaw channels test qqbot
```

## 💬 使用方法

### 发送消息

```bash
# 发送 C2C 消息
openclaw message send --channel qqbot --to "user-openid" --text "Hello!"

# 发送群聊消息
openclaw message send --channel qqbot --to "group-openid" --text "Hello everyone!"

# 发送图片
openclaw message send --channel qqbot --to "user-openid" --image "/path/to/image.jpg"

# 发送语音
openclaw message send --channel qqbot --to "user-openid" --voice "/path/to/voice.mp3"
```

### 接收消息

OpenClaw 会自动接收 QQBot 的消息，你可以通过以下方式查看：

```bash
# 查看最近消息
openclaw messages list --channel qqbot

# 监听实时消息
openclaw messages listen --channel qqbot
```

### 群聊支持

```bash
# 发送到群聊
openclaw message send --channel qqbot --to "group-openid" --text "Hello everyone!"

# 查看群聊成员
openclaw channels members --channel qqbot --group "group-openid"

# 管理群聊权限
openclaw channels permissions qqbot --group "group-openid"
```

## 🔐 安全配置

### Webhook 验证

```json
{
  "channels": {
    "qqbot": {
      "security": {
        "webhookVerification": true,
        "signatureSecret": "your-signature-secret",
        "timestampTolerance": 300
      }
    }
  }
}
```

### 消息加密

```json
{
  "channels": {
    "qqbot": {
      "security": {
        "messageEncryption": true,
        "encryptionKey": "your-encryption-key"
      }
    }
  }
}
```

### 访问控制

```json
{
  "channels": {
    "qqbot": {
      "security": {
        "allowedUsers": ["user-openid-1", "user-openid-2"],
        "deniedUsers": ["user-openid-3"],
        "allowedGroups": ["group-openid-1"],
        "deniedGroups": ["group-openid-2"]
      }
    }
  }
}
```

## 🎨 自定义配置

### 消息模板

```json
{
  "channels": {
    "qqbot": {
      "templates": {
        "welcome": "欢迎使用 OpenClaw 助手！",
        "error": "抱歉，出现了一些问题。",
        "thinking": "正在思考中...",
        "typing": "正在输入..."
      }
    }
  }
}
```

### 自动回复

```json
{
  "channels": {
    "qqbot": {
      "autoReply": {
        "enabled": true,
        "trigger": "mention",
        "delay": 1000,
        "typing": true
      }
    }
  }
}
```

### 消息格式

```json
{
  "channels": {
    "qqbot": {
      "formatting": {
        "markdown": true,
        "codeHighlight": true,
        "linkPreview": true
      }
    }
  }
}
```

### 流式响应

```json
{
  "channels": {
    "qqbot": {
      "streaming": {
        "enabled": true,
        "chunkSize": 100,
        "interval": 100
      }
    }
  }
}
```

## 📤 媒体上传

### 图片上传

```bash
# 上传图片
openclaw media upload --channel qqbot --type image --file "/path/to/image.jpg"

# 发送图片消息
openclaw message send --channel qqbot --to "user-openid" --image "media-id"
```

### 语音上传

```bash
# 上传语音
openclaw media upload --channel qqbot --type voice --file "/path/to/voice.mp3"

# 发送语音消息
openclaw message send --channel qqbot --to "user-openid" --voice "media-id"
```

### 视频上传

```bash
# 上传视频
openclaw media upload --channel qqbot --type video --file "/path/to/video.mp4"

# 发送视频消息
openclaw message send --channel qqbot --to "user-openid" --video "media-id"
```

## 🔍 故障排除

### 常见问题

#### 1. 无法连接 QQBot

**症状**: OpenClaw 无法连接 QQBot

**解决方案**:
```bash
# 检查配置
openclaw config get channels.qqbot

# 检查网络连接
openclaw network test qqbot

# 查看详细日志
openclaw logs qqbot
```

#### 2. 消息发送失败

**症状**: 消息无法发送到 QQBot

**解决方案**:
```bash
# 检查消息配置
openclaw config get channels.qqbot

# 检查 API 凭证
openclaw channels test qqbot

# 重新配置
openclaw channels setup qqbot
```

#### 3. 群聊消息不显示

**症状**: 群聊消息无法接收

**解决方案**:
```bash
# 检查群聊配置
openclaw config get channels.qqbot.allowedGroups

# 检查群聊权限
openclaw channels permissions qqbot

# 重新配置群聊
openclaw channels groups qqbot
```

#### 4. 流式响应不工作

**症状**: 消息无法流式发送

**解决方案**:
```bash
# 检查流式配置
openclaw config get channels.qqbot.streaming

# 重新配置流式
openclaw config set channels.qqbot.streaming.enabled true

# 测试流式响应
openclaw channels test qqbot --streaming
```

### 调试命令

```bash
# 查看 QQBot 渠道状态
openclaw channels status qqbot

# 测试消息发送
openclaw channels test qqbot --message "Test message"

# 查看消息历史
openclaw messages history --channel qqbot

# 重置渠道配置
openclaw channels reset qqbot
```

## 📊 性能优化

### 消息队列

```json
{
  "channels": {
    "qqbot": {
      "queue": {
        "enabled": true,
        "maxSize": 1000,
        "timeout": 5000,
        "retryAttempts": 3
      }
    }
  }
}
```

### 连接池

```json
{
  "channels": {
    "qqbot": {
      "connectionPool": {
        "enabled": true,
        "maxConnections": 10,
        "idleTimeout": 30000,
        "maxRetries": 3
      }
    }
  }
}
```

### 缓存

```json
{
  "channels": {
    "qqbot": {
      "cache": {
        "enabled": true,
        "driver": "memory",
        "ttl": 3600,
        "maxSize": "100MB"
      }
    }
  }
}
```

## 📚 参考资料

- [QQ 开放平台文档](https://q.qq.com/docs)
- [OpenClaw QQBot 集成文档](https://docs.openclaw.ai/zh-CN/channels/qqbot)
- [QQ 机器人 API 参考](https://q.qq.com/docs/api)
- [Webhook 配置指南](https://q.qq.com/docs/webhook)
- [安全配置文档](https://q.qq.com/docs/security)

---

**最后更新**: 2026-05-01
**维护者**: 小毛 🦞
