# NVIDIA 提供商配置指南

**创建时间**: 2026-05-02
**最后更新**: 2026-05-02
**适用版本**: OpenClaw v2026.4.29+

## 📖 概述

NVIDIA 是 OpenClaw v2026.4.29 新增的内置提供商，提供高性能的 AI 模型服务，支持 GPU 加速和多种模型类型。

## 🎯 核心功能

### 主要特性
- **GPU 加速**: 支持 NVIDIA GPU 加速推理
- **模型目录**: 支持静态模型目录
- **API Key 入门**: 支持 API Key 自动配置
- **模型引用**: 支持字面量模型引用选择器

### 支持的模型
- **文本模型**: Llama 3.1, Mixtral, Qwen 等
- **图片模型**: Stable Diffusion XL 等
- **语音模型**: Whisper 等
- **嵌入模型**: BGE, E5 等

## 🔧 基础配置

### 1. 获取 API 密钥

1. 访问 [NVIDIA NGC](https://catalog.ngc.nvidia.com)
2. 注册账号并登录
3. 进入 API Keys 页面
4. 创建新的 API Key
5. 复制 API Key

### 2. 配置 OpenClaw

#### 方法1: 使用命令行

```bash
# 设置 NVIDIA API Key
openclaw config set nvidia.apiKey "your-api-key"

# 验证配置
openclaw config get nvidia
```

#### 方法2: 使用配置文件

在 `~/.openclaw/openclaw.json` 中添加：

```json
{
  "providers": {
    "nvidia": {
      "apiKey": "your-api-key",
      "baseUrl": "https://integrate.api.nvidia.com/v1",
      "models": {
        "default": "nvidia/llama-3.1-70b-instruct",
        "coding": "nvidia/llama-3.1-70b-instruct",
        "fast": "nvidia/llama-3.1-8b-instruct"
      }
    }
  }
}
```

#### 方法3: 使用环境变量

```bash
# 设置环境变量
export NVIDIA_API_KEY="your-api-key"

# 或添加到 .bashrc/.zshrc
echo 'export NVIDIA_API_KEY="your-api-key"' >> ~/.bashrc
source ~/.bashrc
```

### 3. 验证配置

```bash
# 测试 NVIDIA 连接
openclaw provider test nvidia

# 列出可用模型
openclaw models list --provider nvidia

# 测试模型调用
openclaw models test nvidia/llama-3.1-70b-instruct
```

## 🎨 模型配置

### 文本模型

```json
{
  "providers": {
    "nvidia": {
      "models": {
        "text": {
          "default": "nvidia/llama-3.1-70b-instruct",
          "fast": "nvidia/llama-3.1-8b-instruct",
          "powerful": "nvidia/mixtral-8x7b-instruct-v0.1",
          "coding": "nvidia/llama-3.1-70b-instruct"
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
    "nvidia": {
      "models": {
        "image": {
          "default": "nvidia/stable-diffusion-xl-base-1.0",
          "fast": "nvidia/stable-diffusion-turbo",
          "quality": "nvidia/stable-diffusion-3-medium"
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
    "nvidia": {
      "models": {
        "tts": {
          "default": "nvidia/bark",
          "quality": "nvidia/bark-large"
        },
        "stt": {
          "default": "nvidia/whisper-large-v3",
          "fast": "nvidia/whisper-small"
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
    "nvidia": {
      "models": {
        "embedding": {
          "default": "nvidia/bge-large-en-v1.5",
          "multilingual": "nvidia/bge-m3"
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
openclaw image generate --prompt "A beautiful sunset over mountains" --provider nvidia

# 编辑图片
openclaw image edit --input image.png --prompt "Add a rainbow" --provider nvidia
```

### 配置示例

```json
{
  "providers": {
    "nvidia": {
      "media": {
        "imageGeneration": {
          "enabled": true,
          "model": "nvidia/stable-diffusion-xl-base-1.0",
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
openclaw tts synthesize --text "Hello world" --provider nvidia

# 列出可用语音
openclaw tts voices list --provider nvidia
```

### 配置示例

```json
{
  "providers": {
    "nvidia": {
      "tts": {
        "enabled": true,
        "model": "nvidia/bark",
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
openclaw embedding generate --text "Hello world" --provider nvidia

# 计算相似度
openclaw embedding similarity --text1 "Hello" --text2 "Hi" --provider nvidia
```

### 配置示例

```json
{
  "providers": {
    "nvidia": {
      "embedding": {
        "enabled": true,
        "model": "nvidia/bge-large-en-v1.5",
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
| Mixtral 8x7B | 中 | 高 | 中文场景 |
| Stable Diffusion XL | 中 | 高 | 图片生成 |

### 成本控制

```json
{
  "providers": {
    "nvidia": {
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
openclaw usage --provider nvidia

# 查看模型调用次数
openclaw usage --provider nvidia --model nvidia/llama-3.1-70b-instruct

# 导出使用报告
openclaw usage export --provider nvidia --format csv
```

## 🔍 故障排除

### 常见问题

#### 1. API Key 无效

**症状**: 无法连接 NVIDIA

**解决方案**:
```bash
# 检查 API Key 配置
openclaw config get nvidia.apiKey

# 重新配置 API Key
openclaw config set nvidia.apiKey "new-api-key"

# 测试连接
openclaw provider test nvidia
```

#### 2. 模型不可用

**症状**: 模型调用失败

**解决方案**:
```bash
# 列出可用模型
openclaw models list --provider nvidia

# 检查模型配置
openclaw config get nvidia.models

# 更新模型配置
openclaw config set nvidia.models.default "nvidia/llama-3.1-70b-instruct"
```

#### 3. GPU 加速不工作

**症状**: 模型调用缓慢

**解决方案**:
```bash
# 检查 GPU 配置
openclaw config get nvidia.gpu

# 启用 GPU 加速
openclaw config set nvidia.gpu.enabled true

# 检查 GPU 状态
nvidia-smi
```

#### 4. 媒体生成失败

**症状**: 图片生成失败

**解决方案**:
```bash
# 检查媒体生成配置
openclaw config get nvidia.media

# 检查配额
openclaw usage --provider nvidia

# 尝试不同的模型
openclaw image generate --prompt "A cat" --model nvidia/stable-diffusion-turbo
```

### 调试命令

```bash
# 查看 NVIDIA 详细日志
openclaw logs nvidia

# 测试 API 连接
curl -H "Authorization: Bearer your-api-key" https://integrate.api.nvidia.com/v1/models

# 检查网络连接
openclaw network test nvidia
```

## 📚 参考资料

- [NVIDIA NGC 文档](https://docs.nvidia.com)
- [OpenClaw NVIDIA 集成文档](https://docs.openclaw.ai/zh-CN/providers/nvidia)
- [模型目录](https://catalog.ngc.nvidia.com/models)
- [API 参考](https://docs.nvidia.com/nim/index.html)
- [定价信息](https://www.nvidia.com/en-us/data-center/products/)

---

**最后更新**: 2026-05-02
**维护者**: 小毛 🦞
