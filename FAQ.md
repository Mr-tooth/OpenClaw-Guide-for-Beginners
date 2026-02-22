# 常见问题 (FAQ)

> OpenClaw使用中的常见问题和解答

## 📋 目录

- [快速导航](#-快速与其他导航)
- [安装与启动](#-安装与启动)
- [API相关](#-api相关)
- [配置问题](#-配置问题)
- [平台对接](#-平台对接)
- [性能优化](#-性能优化)
- [成本控制](#-成本控制)

---

## 🚀 快速导航

按问题类型快速找到答案：

| 问题类型 | 优先查看 | 相关章节 |
|---------|---------|---------|
| 刚安装 | [快速开始](docs/start/quickstart.md) | 安装与启动 |
| API报错 | [API平台推荐](#q-哪个api平台最推荐) | API相关 |
| 配置失败 | [常见配置错误](#q-如何解决配置错误) | 配置问题 |
| 钉钉/飞书对接 | [平台对接](#q-如何对接钉钉) | 平台对接 |
| 成本过高 | [成本优化](docs/api-config/cost-optimization.md) | 成本控制 |

---

## 🚀 安装与启动

### Q: 如何安装OpenClaw？

**A:** 根据你的系统选择对应方式：

**Windows:**
```powershell
npm install -g openclaw
```

**macOS / Linux:**
```bash
npm install -g openclaw
```

**Docker:**
```bash
docker pull ghcr.io/openclaw/openclaw:latest
```

---

### Q: 安装后如何验证？

**A:** 运行以下命令：
```bash
openclaw --version
```

看到版本号（如 `OpenClaw CLI v2026.2.x`）即安装成功

---

### Q: Gateway启动失败怎么办？

**A:** 检查以下几点：

1. **检查端口占用**
   ```bash
   # Linux/macOS
   lsof -i :18789
   
   # Windows
   netstat -ano | findstr :18789
   ```

2. **检查配置文件**
   ```bash
   openclaw config validate
   ```

3. **查看日志**
   ```bash
   openclaw logs
   ```

4. **重新初始化**
   ```bash
   openclaw init
   ```

详细排查见[故障排除](docs/advanced/troubleshooting.md)

---

## 🔑 API相关

### Q: 哪个API平台最推荐？

**A:** 根据不同需求推荐：

| 需求 | 推荐平台 | 优势 | 链接 |
|------|---------|------|------|
| 新手体验 | 硅基流动 | 注册送2000万Tokens免费 | [🔗](https://cloud.siliconflow.cn/i/lva59yow) |
| 编程开发 | 火山引擎方舟 | 支持Doubao/GLM/DeepSeek/Kimi | [🔗](https://volcengine.com/L/tHxxM_WwYp4/) |
| 开发工具 | 智谱GLM Coding | Claude Code/Cline等20+工具 | [🔗](https://www.bigmodel.cn/glm-coding?ic=BUDVTRHUYH) |
| 长文本处理 | 智谱GLM | 128K上下文，文档总结强 | [🔗](https://z.ai/subscribe) |
| Agent开发 | MiniMax | M2.5优化，多轮对话强 | [🔗](https://platform.minimaxi.com/subscribe/coding-plan) |

---

### Q: 如何获取API密钥？

**A:** 以硅基流动为例：

1. 注册账号：https://cloud.siliconflow.cn/i/lva59yow
2. 进入控制台
3. 创建API Key
4. 复制并保存（只会显示一次）

---

### Q: API密钥如何安全存储？

**A:** OpenClaw自动安全存储：

- 位置：`~/.openclaw/config.json`
- 权限：自动设置为600（仅用户可读写）
- 加密：敏感信息自动加密

**手动设置权限**：
```bash
chmod 600 ~/.openclaw/config.json
```

---

### Q: 怎么降低API使用成本？

**A:** 三种省钱方法：

1. **使用免费额度** - 硅基流动注册送2000万Tokens
   [注册链接](https://cloud.siliconflow.cn/i/lva59yow)

2. **订阅Coding Plan** - 火山引擎首月仅8.9元
   [订阅链接](https://volcengine.com/L/tHxxM_WwYp4/)

3. **年付优惠** - 智谱GLM年付更划算
   [订阅链接](https://z.ai/subscribe)

详见[成本优化指南](docs/api-config/cost-optimization.md)

---

### Q: 免费额度能用多久？

**A:** 硅基流动的2000万Tokens：

| 使用场景 | 每次Token数 | 可用次数 | 大概时长 |
|---------|------------|---------|---------|
| 简单对话 | 50 | 40万次 | 1-3个月 |
| 代码生成 | 300 | 6.6万次 | 1-2个月 |
| 文档处理 | 2000 | 1万次 | 2-4周 |

实际时长取决于使用频率

---

## ☁️ 云服务器相关

### Q: 云服务器配置要求？

**A:** OpenClaw最低配置：

| 配置项 | 最低 | 推荐 | 重度使用 |
|--------|------|------|---------|
| CPU | 1核 | 2核 | 4核 |
| 内存 | 512MB | 2GB | 4-8GB |
| 磁盘 | 10GB | 40GB | 80GB+ |
| 带宽 | 1Mbps | 3Mbps | 5Mbps+ |

**推荐套餐（阿里云）**:
- 2核2G：99元/年（普惠套餐）[🔗](https://www.aliyun.com/activity/ecs/clawdbot?userCode=yyzsc1al)
- 2核4G：120-150元/年
- 4核8G：300-500元/年

---

### Q: 必须购买云服务器吗？

**A:** 不是必须的。

**部署方式对比**:

| 部署方式 | 优势 | 劣势 | 适合人群 |
|---------|------|------|----------|
| 本地部署 | 完全免费 | 离线不可用 | 个人测试 |
| 云服务器 | 24小时在线 | 需要付年费 | 想要稳定服务 |
| [阿里云](https://www.aliyun.com/activity/ecs/clawdbot?userCode=yyzsc1al) | 99元/年超值 | - | 首选 |

---

### Q: 如何在云服务器上部署？

**A:** 详细步骤见[阿里云部署指南](docs/cloud/aliyun-guide.md)

**快速流程**：
1. 购买云服务器
2. SSH连接服务器
3. 安装Node.js
4. 安装OpenClaw
5. 配置API Key
6. 启动Gateway

---

### Q: 云服务器如何保持Gateway运行？

**A:** 使用systemd服务：

```bash
# 创建服务
nano /etc/systemd/system/openclaw.service

# 启动并设置开机自启
systemctl start openclaw
systemctl enable openclaw
```

详细配置见[阿里云部署指南](docs/cloud/aliyun-guide.md)

---

### Q: 云服务器需要开放哪些端口？

**A:** 最小化开放端口：

| 端口 | 用途 | 是否必需 |
|------|------|---------|
| 22 | SSH | ✅ 必需 |
| 18789 | OpenClaw Gateway | ✅ 必需（仅内网） |
| 80/443 | Web访问 | ⚠️ 可选（需配置反向代理） |

**安全建议**：
- 18789端口仅内网访问
- 使用反向代理（Nginx）提供外网访问

---

## 💰 成本相关

### Q: 使用OpenClaw一年要花多少钱？

**A:** 完整成本估算：

| 项目 | 费用 | 优惠方案 |
|------|------|---------|
| 云服务器 | 99元/年 | [阿里云99元套餐](https://www.aliyun.com/activity/ecs/clawdbot?userCode=yyzsc1al) |
| API调用 | 0-480元/年 | 硅基流动免费 / 火山首月8.9元 |
| 域名(可选) | 10元/年 | 首购1元 |
| **总计** | **约100-600元/年** | 通过优惠链接可更低 |

---

### Q: 月花费大概多少？

**A:** 根据使用强度：

| 使用强度 | 服务器 | API | 月费 |
|---------|--------|-----|------|
| 偶尔使用 | 8-10元 | 0元（免费额度） | 8-10元 |
| 日常使用 | 8-10元 | 0-39元 | 8-49元 |
| 重度使用 | 8-10元 | 39-100元 | 47-110元 |
| 专业使用 | 30-40元 | 100-300元 | 130-340元 |

---

## 🤖 功能相关

### Q: OpenClaw能做什么？

**A:** 核心能力：

- ✅ **对话交互**: 自然语言对话，多轮上下文
- ✅ **文件操作**: 读取、编辑、创建文件
- ✅ **Web搜索**: 搜索网络、提取信息
- ✅ **日程管理**: 管理日历、提醒事项
- ✅ **技能系统**: 1700+技能扩展
- ✅ **多平台**: 飞书、钉钉、微信、Telegram等
- ✅ **代码生成**: 编程辅助、代码审查
- ✅ **Agent自主**: 自主规划、执行任务

---

### Q: 如何安装技能？

**A:** 使用ClawHub：

```bash
# 搜索技能
openclaw skills search weather

# 安装技能
openclaw skills install weather

# 查看已安装技能
openclaw skills list
```

详见[技能开发与使用](docs/advanced/skills.md)

---

### Q: 支持哪些平台？

**A:** 已支持的平台：

- ✅ 飞书
- ✅ 钉钉
- ✅ 微信（企业微信）
- ✅ Telegram
- ✅ Discord（开发中）
- ✅ Slack（开发中）
- ✅ Signal（开发中）

---

### Q: 如何切换对话平台？

**A:** 在配置文件中设置：

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "priority": 1
    },
    "dingtalk": {
      "enabled": true,
      "priority": 2
    }
  }
}
```

---

## 🔧 技术相关

### Q: 如何更新OpenClaw？

**A:**
```bash
# 更新到最新版本
npm update -g openclaw

# 或重新安装
npm install -g openclaw@latest

# 验证版本
openclaw --version
```

---

### Q: 如何查看日志？

**A:**
```bash
# 实时查看日志
openclaw logs -f

# 查看最近100行
openclaw logs -n 100

# 查看错误日志
openclaw logs --level error
```

---

### Q: 如何备份数据？

**A:**
```bash
# 备份workspace（包含记忆、配置）
tar -czf openclaw-backup-$(date +%Y%m%d).tar.gz ~/.openclaw/workspace

# 备份完整目录
tar -czf openclaw-full-backup-$(date +%Y%m%d).tar.gz ~/.openclaw
```

---

### Q: 如何迁移到新设备？

**A:**
1. 备份旧设备数据
2. 在新设备安装OpenClaw
3. 恢复备份
4. 更新配置（API Key等）

---

## ❓ 其他问题

### Q: 遇到问题如何获取帮助？

**A:** 多种获取帮助的方式：

1. **查看文档**: 本教程、[官方文档](https://docs.openclaw.ai)
2. **社区支持**: [Discord](https://discord.gg/clawd)
3. **GitHub Issues**: [openclaw/issues](https://github.com/openclaw/openclaw/issues)
4. **AI助手**: 直接问OpenClaw

---

### Q: OpenClaw是免费的吗？

**A:**
- ✅ OpenClaw本身：完全免费开源
- ✅ API调用：各平台有免费额度
- ⚠️ 付费API：按量计费，有优惠套餐
- ⚠️ 云服务器：按月/年付费

详见[成本优化指南](docs/api-config/cost-optimization.md)

---

### Q: 隐私和数据安全？

**A:**
- ✅ 数据存储：全部在本地
- ✅ 加密存储：敏感信息自动加密
- ✅ 访问控制：严格的权限管理
- ✅ 开源透明：代码可审查

详见[安全配置指南](docs/advanced/security.md)

---

### Q: 如何贡献代码？

**A:** 欢迎贡献！

1. Fork项目：[openclaw/openclaw](https://github.com/openclaw/openclaw)
2. 创建功能分支
3. 提交更改
4. 推送到分支
5. 创建Pull Request

---

## 📚 更多资源

- [快速开始](docs/start/quickstart.md)
- [API配置](docs/api-config/api-configuration.md)
- [模型选择](docs/api-config/model-comparison.md)
- [成本优化](docs/api-config/cost-optimization.md)
- [云部署](docs/cloud/cloud-deployment-guide.md)
- [技能开发](docs/advanced/skills.md)
- [故障排除](docs/advanced/troubleshooting.md)

---

**创建时间**: 2026-02-22
**版本**: 1.0
