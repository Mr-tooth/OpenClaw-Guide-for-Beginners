# DeepInfra 提供商配置指南

**创建时间**: 2026-05-01
**最后更新**: 2026-05-01
**适用版本**: OpenClaw v2026.4.27+

## 📖 概述

DeepInfra 是 OpenClaw v2026.4.27 新增的内置提供商，提供高质量的模型服务，支持模型发现、媒体生成、TTS 语音合成和嵌入向量。

## 🎯 核心功能

### 主要特性
- **模型发现**: 自动发现可用模型
- **媒体生成**: 支持图片生成和编辑
- **TTS 语音**: 支持高质量语音合成
- **嵌入向量**: 支持文本嵌入和相似度计算
- **入门引导**: 支持 API Key 自动配置

### 支持的模型
- **文本模型**: Llama 3.1, Mixtral, Qwen 等
- **图片模型**: Stable Diffusion XL, DALL-E 等
- **语音模型**: Whisper, Bark 等
- **嵌入模型**: BGE, E5 等

## 🔧 基础配置

### 1. 获取 API 密钥

1. 访问 [DeepInfra 官网](https://deepinfra.com)
2. 注册账号并登录
3. 进入 API Keys 页面
4. 创建新的 API Key
5. 复制 API Key

### 2. 配置 OpenClaw

#### 方法1: 使用命令行

```bash
# 设置 DeepInfra API Key
openclaw config set deepinfra.apiKey "your-api-key"

# 验证配置
openclaw config get deepinfra
```

#### 方法2: 使用配置文件

在 `~/.openclaw/openclaw.json` 中添加：

```json
{
  "providers": {
    "deepinfra": {
      "apiKey": "your-api-key",
      "baseUrl": "https://api.deepinfra.com/v1/openai",
      "models": {
        "default": "meta-llama/Llama-3.1-70B-Instruct",
        "coding": "Qwen/Qwen2.5-72B-Instruct",
        "vision": "meta-llama/Llama-3.1-70B-Vision"
      }
    }
  }
}
```

#### 方法3: 使用环境变量

```bash
# 设置环境变量
export DEEPINFRA_API_KEY="your-api-key"

# 或添加到 .bashrc/.zshrc
echo 'export DEEPINFRA_API_KEY="your-api-key"' >> ~/.bashrc
source ~/.bashrc
```

### 3. 验证配置

```bash
# 测试 DeepInfra 连接
openclaw provider test deepinfra

# 列出可用模型
openclaw models list --provider deepinfra

# 测试模型调用
openclaw models test meta-llama/Llama-3.1-70B-Instruct
```

## 🎨 模型配置

### 文本模型

```json
{
  "providers": {
    "deepinfra": {
      "models": {
        "text": {
          "default": "meta-llama/Llama-3.1-70B-Instruct",
          "fast": "meta-llama/Llama-3.1-8B-Instruct",
          "powerful": "Qwen/Qwen2.5-72B-Instruct",
          "coding": "Qwen/Qwen2.5-Coder-32B-Instruct"
        }
      }
    }
  }
}
```

### 图片模型

```json
{
  "providers": {
    "deepinfra": {
      "models": {
        "image": {
          "default": "stabilityai/stable-diffusion-xl-base-1.0",
          "fast": "stabilityai/stable-diffusion-turbo",
          "quality": "stabilityai/stable-diffusion-3-medium"
        }
      }
    }
  }
}
```

### 语音模型

```json
{
  "providers": {
    "deepinfra": {
      "models": {
        "tts": {
          "default": "bark",
          "quality": "bark-large"
        },
        "stt": {
          "default": "openai/whisper-large-v3",
          "fast": "openai/whisper-small"
        }
      }
    }
  }
}
```

### 嵌入模型

```json
{
  "providers": {
    "deepinfra": {
      "models": {
        "embedding": {
          "default": "BAAI/bge-large-en-v1.5",
          "multilingual": "BAAI/bge-m3"
        }
      }
    }
  }
}
```

## 🖼️ 媒体生成配置

### 图片生成

```bash
# 生成图片
openclaw image generate --prompt "A beautiful sunset over mountains" --provider deepinfra

# 编辑图片
openclaw image edit --input image.png --prompt "Add a rainbow" --provider deepinfra
```

### 配置示例

```json
{
  "providers": {
    "deepinfra": {
      "media": {
        "imageGeneration": {
          "enabled": true,
          "model": "stabilityai/stable-diffusion-xl-base-1.0",
          "defaultParams": {
            "steps": 30,
            "cfgScale": 7.5,
            "width": 1024,
            "height": 1024
          }
        }
      }
    }
  }
}
```

## 🎤 TTS 语音配置

### 语音合成

```bash
# 合成语音
openclaw tts synthesize --text "Hello world" --provider deepinfra

# 列出可用语音
openclaw tts voices list --provider deepinfra
```

### 配置示例

```json
{
  "providers": {
    "deepinfra": {
      "tts": {
        "enabled": true,
        "model": "bark",
        "defaultVoice": "v2/en_speaker_6",
        "sampleRate": 22050
      }
    }
  }
}
```

## 📊 嵌入向量配置

### 文本嵌入

```bash
# 生成嵌入向量
openclaw embedding generate --text "Hello world" --provider deepinfra

# 计算相似度
openclaw embedding similarity --text1 "Hello" --text2 "Hi" --provider deepinfra
```

### 配置示例

```json
{
  "providers": {
    "deepinfra": {
      "embedding": {
        "enabled": true,
        "model": "BAAI/bge-large-en-v1.5",
        "dimensions": 1024,
        "batchSize": 32
      }
    }
  }
}
```

## 💰 成本优化

### 模型选择建议

| 模型 | 价格 | 性能 | 推荐场景 |
|------|------|------|----------|
| Llama 3.1 8B | 低 | 中 | 日常对话 |
| Llama 3.1 70B | 中 | 高 | 复杂任务 |
| Qwen 2.5 72B | 中 | 高 | 中文场景 |
| Stable Diffusion XL | 中 | 高 | 图片生成 |

### 成本控制

```json
{
  "providers": {
    "deepinfra": {
      "costControl": {
        "enabled": true,
        "monthlyLimit": 100,
        "alertThreshold": 80,
        "alertEmail": "your-email@example.com"
      }
    }
  }
}
```

### 使用统计

```bash
# 查看使用统计
openclaw usage --provider deepinfra

# 查看模型调用次数
openclaw usage --provider deepinfra --model meta-llama/Llama-3.1-70B-Instruct

# 导出使用报告
openclaw usage export --provider deepinfra --format csv
```

## 🔍 故障排除

### 常见问题

#### 1. API Key 无效

**症状**: 无法连接 DeepInfra

**解决方案**:
```bash
# 检查 API Key 配置
openclaw config get deepinfra.apiKey

# 重新配置 API Key
openclaw config set deepinfra.apiKey "new-api-key"

# 测试连接
openclaw provider test deepinfra
```

#### 2. 模型不可用

**症状**: 模型调用失败

**解决方案**:
```bash
# 列出可用模型
openclaw models list --provider deepinfra

# 检查模型配置
openclaw config get deepinfra.models

# 更新模型配置
openclaw config set deepinfra.models.default "meta-llama/Llama-3.1-70B-Instruct"
```

#### 3. 媒体生成失败

**症状**: 图片生成失败

**解决方案**:
```bash
# 检查媒体生成配置
openclaw config get deepinfra.media

# 检查配额
openclaw usage --provider deepinfra

# 尝试不同的模型
openclaw image generate --prompt "A cat" --model stabilityai/stable-diffusion-turbo
```

#### 4. TTS 语音质量问题

**症状**: 语音合成不自然

**解决方案**:
```bash
# 尝试不同的语音模型
openclaw tts synthesize --text "Hello" --model bark-large

# 调整语音参数
openclaw config set deepinfra.tts.sampleRate 44100
```

### 调试命令

```bash
# 查看 DeepInfra 详细日志
openclaw logs deepinfra

# 测试 API 连接
curl -H "Authorization: Bearer your-api-key" https://api.deepinfra.com/v1/openai/models

# 检查网络连接
openclaw network test deepinfra
```

## 📚 参考资料

- [DeepInfra 官方文档](https://deepinfra.com/docs)
- [OpenClaw DeepInfra 集成文档](https://docs.openclaw.ai/providers/deepinfra)
- [模型目录](https://deepinfra.com/models)
- [API 参考](https://deepinfra.com/docs/api-reference)
- [定价信息](https://deepinfra.com/pricing)

---

**最后更新**: 2026-05-01
**维护者**: 小毛 🦞
