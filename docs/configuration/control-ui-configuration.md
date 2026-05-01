# Control UI 配置指南

**创建时间**: 2026-05-01
**最后更新**: 2026-05-01
**适用版本**: OpenClaw v2026.4.26+

## 📖 概述

OpenClaw v2026.4.26 引入了全新的 Control UI，提供图形化界面管理和配置 OpenClaw。本指南将帮助你配置和使用 Control UI。

## 🎯 核心功能

### 主要特性
- **图形化界面**: Web 界面管理和配置 OpenClaw
- **实时监控**: 实时查看 Gateway 状态和日志
- **配置编辑**: 可视化编辑配置文件
- **Talk 工作流**: 支持语音对话和实时交互
- **PWA 支持**: 可安装为渐进式 Web 应用

### 新增功能
- **Control UI/Talk 工作流**: 实时语音对话
- **Google Meet 集成**: 会议记录和管理
- **Cerebras 提供商**: 新的模型提供商支持
- **迁移工具**: 从旧版本迁移配置

## 🔧 基础配置

### 1. 启用 Control UI

在 `~/.openclaw/openclaw.json` 中添加 Control UI 配置：

```json
{
  "controlUI": {
    "enabled": true,
    "port": 8080,
    "host": "0.0.0.0",
    "auth": {
      "enabled": true,
      "username": "admin",
      "password": "your-secure-password"
    }
  }
}
```

### 2. 使用命令行配置

```bash
# 启用 Control UI
openclaw config set controlUI.enabled true

# 设置端口
openclaw config set controlUI.port 8080

# 设置监听地址
openclaw config set controlUI.host 0.0.0.0

# 启用认证
openclaw config set controlUI.auth.enabled true

# 设置用户名
openclaw config set controlUI.auth.username admin

# 设置密码
openclaw config set controlUI.auth.password "your-secure-password"
```

### 3. 启动 Control UI

```bash
# 启动 Control UI
openclaw control-ui start

# 查看状态
openclaw control-ui status

# 停止 Control UI
openclaw control-ui stop
```

## 🖥️ 访问 Control UI

### 本地访问

```bash
# 默认访问地址
http://localhost:8080

# 使用认证
http://admin:your-secure-password@localhost:8080
```

### 远程访问

```bash
# 使用服务器 IP
http://your-server-ip:8080

# 使用域名（推荐）
https://your-domain.com:8080
```

### PWA 安装

1. 访问 Control UI 界面
2. 点击浏览器地址栏的"安装"按钮
3. 确认安装 PWA

## 💬 Talk 工作流配置

### 启用 Talk 功能

```json
{
  "controlUI": {
    "talk": {
      "enabled": true,
      "transport": "websocket",
      "codec": "opus",
      "sampleRate": 48000
    }
  }
}
```

### 配置语音对话

```bash
# 启用 Talk 功能
openclaw config set controlUI.talk.enabled true

# 设置传输协议
openclaw config set controlUI.talk.transport websocket

# 设置音频编解码器
openclaw config set controlUI.talk.codec opus

# 设置采样率
openclaw config set controlUI.talk.sampleRate 48000
```

### Google Meet 集成

```json
{
  "controlUI": {
    "googleMeet": {
      "enabled": true,
      "calendarId": "primary",
      "autoJoin": false,
      "recordMeeting": true
    }
  }
}
```

## 🔐 安全配置

### 认证配置

```json
{
  "controlUI": {
    "auth": {
      "enabled": true,
      "method": "basic",
      "username": "admin",
      "password": "your-secure-password",
      "sessionTimeout": "24h"
    }
  }
}
```

### HTTPS 配置

```json
{
  "controlUI": {
    "ssl": {
      "enabled": true,
      "cert": "/path/to/cert.pem",
      "key": "/path/to/key.pem"
    }
  }
}
```

### 访问控制

```json
{
  "controlUI": {
    "access": {
      "allowedIPs": ["192.168.1.0/24", "10.0.0.0/8"],
      "deniedIPs": [],
      "rateLimit": {
        "enabled": true,
        "maxRequests": 100,
        "windowMs": 60000
      }
    }
  }
}
```

## 📊 监控和日志

### 实时监控

```bash
# 查看 Gateway 状态
openclaw control-ui status

# 查看实时日志
openclaw control-ui logs

# 查看资源使用
openclaw control-ui stats
```

### 日志配置

```json
{
  "controlUI": {
    "logging": {
      "enabled": true,
      "level": "info",
      "file": "/var/log/openclaw/control-ui.log",
      "maxSize": "100MB",
      "maxFiles": 5
    }
  }
}
```

## 🔧 高级配置

### WebSocket 配置

```json
{
  "controlUI": {
    "websocket": {
      "enabled": true,
      "path": "/ws",
      "heartbeat": 30000,
      "maxConnections": 100
    }
  }
}
```

### API 配置

```json
{
  "controlUI": {
    "api": {
      "enabled": true,
      "path": "/api",
      "cors": {
        "enabled": true,
        "origins": ["*"]
      }
    }
  }
}
```

### 缓存配置

```json
{
  "controlUI": {
    "cache": {
      "enabled": true,
      "driver": "memory",
      "ttl": 3600,
      "maxSize": "100MB"
    }
  }
}
```

## 🎨 界面自定义

### 主题配置

```json
{
  "controlUI": {
    "theme": {
      "primary": "#1976d2",
      "secondary": "#9c27b0",
      "background": "#ffffff",
      "text": "#000000",
      "darkMode": false
    }
  }
}
```

### 布局配置

```json
{
  "controlUI": {
    "layout": {
      "sidebar": {
        "collapsed": false,
        "width": 250
      },
      "header": {
        "fixed": true,
        "height": 64
      },
      "footer": {
        "fixed": true,
        "height": 48
      }
    }
  }
}
```

## 📱 移动端支持

### 响应式设计

Control UI 支持响应式设计，可以在移动设备上使用：

- **手机**: 完整功能支持
- **平板**: 优化布局
- **桌面**: 完整功能支持

### PWA 安装

1. 在移动设备上访问 Control UI
2. 点击"添加到主屏幕"
3. 确认安装

## 🔍 故障排除

### 常见问题

#### 1. Control UI 无法访问

**症状**: 无法打开 Control UI 界面

**解决方案**:
```bash
# 检查 Control UI 状态
openclaw control-ui status

# 检查端口占用
netstat -tulpn | grep 8080

# 检查防火墙
sudo ufw allow 8080

# 重启 Control UI
openclaw control-ui restart
```

#### 2. 认证失败

**症状**: 输入用户名密码后无法登录

**解决方案**:
```bash
# 检查认证配置
openclaw config get controlUI.auth

# 重置密码
openclaw config set controlUI.auth.password "new-password"

# 重启 Control UI
openclaw control-ui restart
```

#### 3. Talk 功能不工作

**症状**: 无法进行语音对话

**解决方案**:
```bash
# 检查 Talk 配置
openclaw config get controlUI.talk

# 检查音频设备
openclaw control-ui audio-test

# 重启 Control UI
openclaw control-ui restart
```

#### 4. Google Meet 集成失败

**症状**: 无法加入 Google Meet 会议

**解决方案**:
```bash
# 检查 Google Meet 配置
openclaw config get controlUI.googleMeet

# 重新授权 Google 账号
openclaw control-ui google-auth

# 检查日历权限
openclaw control-ui calendar-test
```

### 调试命令

```bash
# 查看 Control UI 详细日志
openclaw control-ui logs --verbose

# 测试 Control UI 连接
openclaw control-ui test

# 检查配置有效性
openclaw config validate

# 重置 Control UI 配置
openclaw config unset controlUI
```

## 📊 性能优化

### 缓存优化

```json
{
  "controlUI": {
    "cache": {
      "enabled": true,
      "driver": "redis",
      "host": "localhost",
      "port": 6379,
      "ttl": 3600
    }
  }
}
```

### 并发优化

```json
{
  "controlUI": {
    "concurrency": {
      "maxConnections": 100,
      "maxRequests": 1000,
      "timeout": 30000
    }
  }
}
```

### 负载均衡

```json
{
  "controlUI": {
    "loadBalancer": {
      "enabled": true,
      "algorithm": "round-robin",
      "healthCheck": {
        "enabled": true,
        "interval": 10000,
        "path": "/health"
      }
    }
  }
}
```

## 📚 参考资料

- [Control UI 官方文档](https://docs.openclaw.ai/features/control-ui)
- [Talk 工作流文档](https://docs.openclaw.ai/features/talk)
- [Google Meet 集成文档](https://docs.openclaw.ai/integrations/google-meet)
- [安全配置文档](https://docs.openclaw.ai/security)
- [性能优化文档](https://docs.openclaw.ai/performance)

---

**最后更新**: 2026-05-01
**维护者**: 小毛 🦞
