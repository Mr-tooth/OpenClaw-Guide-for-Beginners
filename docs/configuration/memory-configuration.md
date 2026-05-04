# 记忆系统配置指南

**创建时间**: 2026-05-02
**最后更新**: 2026-05-02
**适用版本**: OpenClaw v2026.4.29+

## 📖 概述

OpenClaw v2026.4.29 全面升级了记忆系统，新增 People-aware Wiki、Active Memory 和部分召回功能，提供更智能的记忆管理。

## 🎯 核心功能

### 主要特性
- **People-aware Wiki**: 人员感知的 Wiki 功能
- **Active Memory**: 主动记忆管理
- **部分召回**: 超时部分召回功能
- **诊断工具**: REM 预览诊断

### 记忆类型
- **短期记忆**: 会话内的临时记忆
- **长期记忆**: 跨会话的持久记忆
- **人员记忆**: 人员相关信息
- **主动记忆**: 智能记忆管理

## 🔧 基础配置

### 1. 启用记忆系统

在 `~/.openclaw/openclaw.json` 中添加记忆系统配置：

```json
{
  "memory": {
    "enabled": true,
    "type": "active",
    "storage": "sqlite",
    "maxSize": "1GB",
    "ttl": "30d"
  }
}
```

### 2. 使用命令行配置

```bash
# 启用记忆系统
openclaw config set memory.enabled true

# 设置记忆类型
openclaw config set memory.type active

# 设置存储方式
openclaw config set memory.storage sqlite

# 设置最大大小
openclaw config set memory.maxSize 1GB

# 设置过期时间
openclaw config set memory.ttl 30d
```

### 3. 验证配置

```bash
# 查看记忆系统状态
openclaw memory status

# 测试记忆功能
openclaw memory test

# 查看记忆统计
openclaw memory stats
```

## 👥 People-aware Wiki

### 启用 People Wiki

```json
{
  "memory": {
    "wiki": {
      "enabled": true,
      "provenance": true,
      "aliases": true,
      "relationships": true
    }
  }
}
```

### 配置人员信息

```bash
# 添加人员信息
openclaw memory wiki add-person --name "John Doe" --email "john@example.com"

# 查看人员信息
openclaw memory wiki get-person --name "John Doe"

# 更新人员信息
openclaw memory wiki update-person --name "John Doe" --phone "1234567890"

# 删除人员信息
openclaw memory wiki delete-person --name "John Doe"
```

### 人员关系管理

```bash
# 添加关系
openclaw memory wiki add-relationship --from "John Doe" --to "Jane Doe" --type "colleague"

# 查看关系
openclaw memory wiki get-relationships --name "John Doe"

# 删除关系
openclaw memory wiki delete-relationship --from "John Doe" --to "Jane Doe"
```

### 来源视图

```bash
# 查看人员来源
openclaw memory wiki provenance --name "John Doe"

# 查看关系来源
openclaw memory wiki provenance --relationship "John Doe" --to "Jane Doe"
```

## 🧠 Active Memory

### 启用 Active Memory

```json
{
  "memory": {
    "active": {
      "enabled": true,
      "filters": {
        "allowedChatIds": [],
        "deniedChatIds": []
      },
      "recall": {
        "enabled": true,
        "timeout": 30000,
        "maxItems": 100
      }
    }
  }
}
```

### 配置会话过滤器

```bash
# 添加允许的会话
openclaw memory active add-allowed-chat --chat-id "chat-123"

# 添加拒绝的会话
openclaw memory active add-denied-chat --chat-id "chat-456"

# 查看过滤器
openclaw memory active get-filters

# 清除过滤器
openclaw memory active clear-filters
```

### 配置部分召回

```bash
# 启用部分召回
openclaw config set memory.active.recall.enabled true

# 设置超时时间
openclaw config set memory.active.recall.timeout 30000

# 设置最大项目数
openclaw config set memory.active.recall.maxItems 100
```

## 🔄 部分召回功能

### 启用部分召回

```json
{
  "memory": {
    "recall": {
      "enabled": true,
      "timeout": 30000,
      "maxItems": 100,
      "strategy": "smart"
    }
  }
}
```

### 配置召回策略

```bash
# 设置召回策略
openclaw config set memory.recall.strategy smart

# 查看召回统计
openclaw memory recall stats

# 测试召回功能
openclaw memory recall test
```

### 召回策略选项

- **smart**: 智能召回，根据相关性选择
- **recent**: 最近召回，选择最新的记忆
- **frequent**: 频繁召回，选择最常访问的记忆
- **random**: 随机召回，随机选择记忆

## 🔍 诊断工具

### REM 预览诊断

```bash
# 查看 REM 预览
openclaw memory diagnostic rem-preview

# 运行诊断
openclaw memory diagnostic run

# 查看诊断报告
openclaw memory diagnostic report
```

### 记忆健康检查

```bash
# 检查记忆健康状态
openclaw memory health

# 修复记忆问题
openclaw memory repair

# 优化记忆存储
openclaw memory optimize
```

### 记忆统计

```bash
# 查看记忆统计
openclaw memory stats

# 查看存储使用情况
openclaw memory storage

# 查看访问日志
openclaw memory access-log
```

## 📊 性能优化

### 缓存配置

```json
{
  "memory": {
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

### 索引优化

```json
{
  "memory": {
    "index": {
      "enabled": true,
      "type": "vector",
      "dimensions": 1536,
      "metric": "cosine"
    }
  }
}
```

### 存储优化

```json
{
  "memory": {
    "storage": {
      "type": "sqlite",
      "wal": true,
      "cacheSize": "64MB",
      "journalMode": "delete"
    }
  }
}
```

## 🔐 安全配置

### 访问控制

```json
{
  "memory": {
    "security": {
      "enabled": true,
      "allowedUsers": ["user-1", "user-2"],
      "deniedUsers": ["user-3"],
      "encryption": true,
      "encryptionKey": "your-encryption-key"
    }
  }
}
```

### 审计日志

```json
{
  "memory": {
    "audit": {
      "enabled": true,
      "logAccess": true,
      "logModifications": true,
      "logDeletions": true
    }
  }
}
```

## 🔍 故障排除

### 常见问题

#### 1. 记忆系统不工作

**症状**: 无法保存或检索记忆

**解决方案**:
```bash
# 检查记忆系统状态
openclaw memory status

# 检查存储空间
openclaw memory storage

# 重启记忆系统
openclaw memory restart
```

#### 2. People Wiki 显示错误

**症状**: 人员信息显示错误

**解决方案**:
```bash
# 检查 Wiki 配置
openclaw config get memory.wiki

# 重建 Wiki 索引
openclaw memory wiki rebuild

# 验证 Wiki 数据
openclaw memory wiki verify
```

#### 3. Active Memory 过滤器不工作

**症状**: 会话过滤器不生效

**解决方案**:
```bash
# 检查过滤器配置
openclaw config get memory.active.filters

# 重置过滤器
openclaw memory active clear-filters

# 重新配置过滤器
openclaw memory active add-allowed-chat --chat-id "chat-123"
```

#### 4. 部分召回失败

**症状**: 部分召回功能不工作

**解决方案**:
```bash
# 检查召回配置
openclaw config get memory.recall

# 测试召回功能
openclaw memory recall test

# 查看召回日志
openclaw memory recall logs
```

### 调试命令

```bash
# 查看记忆系统详细日志
openclaw logs memory

# 测试记忆功能
openclaw memory test

# 查看记忆统计
openclaw memory stats

# 重置记忆系统
openclaw memory reset
```

## 📚 参考资料

- [记忆系统官方文档](https://docs.openclaw.ai/zh-CN/features/memory)
- [People-aware Wiki 文档](https://docs.openclaw.ai/zh-CN/features/memory/wiki)
- [Active Memory 文档](https://docs.openclaw.ai/zh-CN/features/memory/active)
- [部分召回文档](https://docs.openclaw.ai/zh-CN/features/memory/recall)
- [诊断工具文档](https://docs.openclaw.ai/zh-CN/features/memory/diagnostics)

---

**最后更新**: 2026-05-02
**维护者**: 小毛 🦞
