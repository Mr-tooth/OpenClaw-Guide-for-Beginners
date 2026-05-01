# TTS 语音配置指南

**创建时间**: 2026-05-01
**最后更新**: 2026-05-01
**适用版本**: OpenClaw v2026.4.25+

## 📖 概述

OpenClaw v2026.4.25 全面升级了 TTS（Text-to-Speech）语音系统，支持多种语音提供商和高级功能。本指南将帮助你配置和使用 TTS 功能。

## 🎯 核心功能

### 主要特性
- **多提供商支持**: Azure Speech、Xiaomi、Volcengine、ElevenLabs 等
- **语音角色**: 支持个性化语音角色配置
- **会话级控制**: 每个聊天可以独立配置 TTS
- **自动语音**: 支持自动将消息转换为语音

### 新增命令
- `/tts latest` - 语音朗读最新消息
- `/tts on` - 开启自动 TTS
- `/tts off` - 关闭自动 TTS
- `/tts voice <voice_name>` - 切换语音角色

## 🔧 基础配置

### 1. 配置 TTS 提供商

在 `~/.openclaw/openclaw.json` 中添加 TTS 配置：

```json
{
  "tts": {
    "enabled": true,
    "provider": "azure",
    "voice": "zh-CN-XiaoxiaoNeural",
    "autoTts": false
  }
}
```

### 2. 使用命令行配置

```bash
# 启用 TTS
openclaw config set tts.enabled true

# 设置提供商
openclaw config set tts.provider azure

# 设置语音角色
openclaw config set tts.voice zh-CN-XiaoxiaoNeural

# 关闭自动 TTS
openclaw config set tts.autoTts false
```

### 3. 验证配置

```bash
# 查看 TTS 配置
openclaw config get tts

# 测试 TTS 功能
/tts latest
```

## 🎤 提供商配置

### Azure Speech (推荐)

Azure Speech 是微软提供的高质量语音服务，支持多种语言和语音角色。

#### 配置步骤

1. **获取 API 密钥**
   - 访问 [Azure Portal](https://portal.azure.com)
   - 创建 Speech 资源
   - 获取 API 密钥和区域

2. **配置 OpenClaw**
   ```bash
   # 设置 Azure Speech 配置
   openclaw config set tts.provider azure
   openclaw config set tts.azure.apiKey "your-api-key"
   openclaw config set tts.azure.region "eastasia"
   ```

3. **选择语音角色**
   ```bash
   # 中文女声
   openclaw config set tts.voice zh-CN-XiaoxiaoNeural
   
   # 中文男声
   openclaw config set tts.voice zh-CN-YunxiNeural
   
   # 英文女声
   openclaw config set tts.voice en-US-JennyNeural
   ```

#### 支持的语音角色

| 语言 | 女声 | 男声 |
|------|------|------|
| 中文 | zh-CN-XiaoxiaoNeural | zh-CN-YunxiNeural |
| 英文 | en-US-JennyNeural | en-US-GuyNeural |
| 日文 | ja-JP-NanamiNeural | ja-JP-KeitaNeural |
| 韩文 | ko-KR-SunHiNeural | ko-KR-InJoonNeural |

### Xiaomi (小米语音)

小米语音合成是小米提供的中文语音服务，适合中文场景。

#### 配置步骤

1. **获取 API 密钥**
   - 访问 [小米 MiMo 开放平台](https://platform.xiaomimimo.com)
   - 申请 TTS API 访问权限
   - 获取 API 密钥

2. **配置 OpenClaw**
   ```bash
   # 设置 Xiaomi 配置
   openclaw config set tts.provider xiaomi
   openclaw config set tts.xiaomi.apiKey "your-api-key"
   ```

3. **选择语音角色**
   ```bash
   # 中文女声
   openclaw config set tts.voice xiaomi-female
   
   # 中文男声
   openclaw config set tts.voice xiaomi-male
   ```

### Volcengine (火山引擎)

火山引擎是字节跳动提供的云服务，支持高质量中文语音合成。

#### 配置步骤

1. **获取 API 密钥**
   - 访问 [火山引擎控制台](https://console.volcengine.com)
   - 开通语音合成服务
   - 获取 API 密钥和 App ID

2. **配置 OpenClaw**
   ```bash
   # 设置 Volcengine 配置
   openclaw config set tts.provider volcengine
   openclaw config set tts.volcengine.apiKey "your-api-key"
   openclaw config set tts.volcengine.appId "your-app-id"
   ```

3. **选择语音角色**
   ```bash
   # 中文女声
   openclaw config set tts.voice volcengine-female
   
   # 中文男声
   openclaw config set tts.voice volcengine-male
   ```

### ElevenLabs v3

ElevenLabs 提供高质量的语音合成，支持语音克隆和情感控制。

#### 配置步骤

1. **获取 API 密钥**
   - 访问 [ElevenLabs](https://elevenlabs.io)
   - 注册账号并获取 API 密钥

2. **配置 OpenClaw**
   ```bash
   # 设置 ElevenLabs 配置
   openclaw config set tts.provider elevenlabs
   openclaw config set tts.elevenlabs.apiKey "your-api-key"
   ```

3. **选择语音角色**
   ```bash
   # 使用预设语音
   openclaw config set tts.voice elevenlabs-rachel
   
   # 使用自定义语音（需要先克隆）
   openclaw config set tts.voice elevenlabs-custom-id
   ```

## 🎭 语音角色配置

### 使用预设角色

OpenClaw 提供多种预设语音角色：

```bash
# 查看可用语音角色
openclaw tts voices list

# 使用预设角色
openclaw config set tts.voice zh-CN-XiaoxiaoNeural
```

### 自定义语音角色

#### ElevenLabs 语音克隆

1. **上传音频样本**
   ```bash
   # 上传音频文件进行克隆
   openclaw tts clone --name "my-voice" --file "sample.wav"
   ```

2. **使用克隆的语音**
   ```bash
   # 使用自定义语音
   openclaw config set tts.voice "cloned:my-voice"
   ```

#### SSML 语音控制

使用 SSML（Speech Synthesis Markup Language）控制语音效果：

```xml
<speak>
  <prosody rate="slow" pitch="+10%">
    这是一个慢速高音的示例。
  </prosody>
  
  <break time="500ms"/>
  
  <prosody rate="fast" pitch="-10%">
    这是一个快速低音的示例。
  </prosody>
</speak>
```

## 🔄 自动 TTS 配置

### 会话级自动 TTS

在聊天中开启自动 TTS：

```bash
# 开启当前会话自动 TTS
/tts on

# 关闭当前会话自动 TTS
/tts off

# 查看当前会话 TTS 状态
/tts status
```

### 全局自动 TTS

配置全局自动 TTS：

```bash
# 开启全局自动 TTS
openclaw config set tts.autoTts true

# 关闭全局自动 TTS
openclaw config set tts.autoTts false
```

### 代理级自动 TTS

为特定代理配置自动 TTS：

```json
{
  "agents": {
    "defaults": {
      "tts": {
        "autoTts": true,
        "voice": "zh-CN-XiaoxiaoNeural"
      }
    }
  }
}
```

## 💬 WhatsApp TTS 集成

### 语音朗读最新消息

在 WhatsApp 中使用 TTS：

```bash
# 朗读最新消息
/tts latest

# 朗读指定数量的消息
/tts latest 5
```

### 自动语音回复

配置 WhatsApp 自动语音回复：

```json
{
  "channels": {
    "whatsapp": {
      "tts": {
        "autoReply": true,
        "voice": "zh-CN-XiaoxiaoNeural"
      }
    }
  }
}
```

## 🔍 故障排除

### 常见问题

#### 1. TTS 不工作

**症状**: 使用 `/tts` 命令没有声音

**解决方案**:
```bash
# 检查 TTS 配置
openclaw config get tts

# 检查提供商配置
openclaw config get tts.azure  # 或其他提供商

# 测试提供商连接
openclaw tts test
```

#### 2. 语音质量差

**症状**: 合成的语音不自然

**解决方案**:
- 尝试不同的语音角色
- 调整语速和音调参数
- 升级到更高质量的提供商

#### 3. 延迟高

**症状**: TTS 合成需要很长时间

**解决方案**:
- 使用本地 CLI 提供商
- 选择更快的语音角色
- 检查网络连接

#### 4. 语言支持问题

**症状**: 某些语言不支持

**解决方案**:
- 检查提供商的语言支持列表
- 使用支持目标语言的提供商
- 考虑使用多语言提供商

### 调试命令

```bash
# 查看 TTS 详细日志
openclaw logs tts

# 测试 TTS 提供商
openclaw tts test --provider azure

# 查看可用语音
openclaw tts voices list --provider azure

# 重置 TTS 配置
openclaw config unset tts
```

## 📊 性能优化

### 选择合适的提供商

| 提供商 | 延迟 | 质量 | 价格 | 推荐场景 |
|--------|------|------|------|----------|
| Azure Speech | 低 | 高 | 中 | 企业级应用 |
| Xiaomi | 低 | 中 | 低 | 中文场景 |
| Volcengine | 低 | 高 | 中 | 中文场景 |
| ElevenLabs | 中 | 极高 | 高 | 高质量需求 |
| Local CLI | 极低 | 中 | 免费 | 本地部署 |

### 缓存优化

启用 TTS 缓存减少重复合成：

```json
{
  "tts": {
    "cache": {
      "enabled": true,
      "maxSize": "100MB",
      "ttl": "7d"
    }
  }
}
```

### 并发控制

配置并发 TTS 请求：

```json
{
  "tts": {
    "concurrency": {
      "max": 5,
      "queue": true
    }
  }
}
```

## 🔐 安全考虑

### API 密钥安全

- 使用环境变量存储 API 密钥
- 定期轮换 API 密钥
- 限制 API 密钥权限

```bash
# 使用环境变量
export TTS_API_KEY="your-api-key"
openclaw config set tts.azure.apiKey "$TTS_API_KEY"
```

### 访问控制

配置 TTS 访问控制：

```json
{
  "tts": {
    "access": {
      "allowedUsers": ["user1", "user2"],
      "deniedUsers": ["user3"]
    }
  }
}
```

## 📚 参考资料

- [Azure Speech 文档](https://docs.microsoft.com/azure/cognitive-services/speech-service/)
- [小米 MiMo TTS 文档](https://platform.xiaomimimo.com/docs/tts)
- [火山引擎 TTS 文档](https://www.volcengine.com/docs/6561)
- [ElevenLabs 文档](https://elevenlabs.io/docs)
- [SSML 参考](https://docs.microsoft.com/azure/cognitive-services/speech-service/ssml-reference)

---

**最后更新**: 2026-05-01
**维护者**: 小毛 🦞
