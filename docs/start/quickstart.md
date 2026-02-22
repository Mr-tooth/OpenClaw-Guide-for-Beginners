# 5分钟快速上手

> 在5分钟内完成OpenClaw的安装和配置，开始你的AI助手之旅

---

## 📋 第1步：获取API密钥 ⭐

OpenClaw需要接入大模型API才能运行。推荐使用以下平台：

### 推荐方案

#### 方案1: 硅基流动（新手推荐）

✅ **优势**: 注册即送2000万Tokens，完全免费体验

[🔗 注册硅基流动 - 领取免费额度](https://cloud.siliconflow.cn/i/lva59yow)
**邀请码**: `lva59yow`

**注册后获取API Key**:
1. 进入控制台
2. 创建API Key
3. 复制备用

---

#### 方案2: 火山引擎方舟（高性价比）

✅ **优势**: 支持Doubao、GLM、DeepSeek、Kimi等模型，工具不限，折上9折低至8.9元

[🔗 订阅火山引擎Coding Plan](https://volcengine.com/L/tHxxM_WwYp4/)
**邀请码**: `XCWPZTHW`

**套餐选择**:
- 首月8.9元起
- 订阅越多越划算
- 支持20+大编程工具（Claude Code、Cline等）

---

#### 方案3: 智谱GLM Coding（编程友好）

✅ **优势**: 专为编程优化，Claude Code、Cline等20+工具无缝支持

[🔗 立即开拼 - 享限时惊喜价](https://www.bigmodel.cn/glm-coding?ic=BUDVTRHUYH)

**核心卖点**:
- 越拼越爽，码力全开
- 限时惊喜价
- 邀你一起薅羊毛

---

## 📋 第2步：安装OpenClaw

### Windows

```powershell
# 使用npm安装（推荐）
npm install -g openclaw

# 或使用npx（无需安装）
npx openclaw install
```

### macOS / Linux

```bash
# 使用npm安装
npm install -g openclaw

# 验证安装
openclaw --version
```

### 验证安装

运行以下命令验证安装成功：

```bash
openclaw --version
```

✅ 成功标志：看到版本号（如 `OpenClaw CLI v2026.2.x`）

---

## 📋 第3步：配置API密钥

```bash
# 启动配置向导
openclaw init
```

按照提示操作：
1. 选择API提供商
2. 粘贴API Key
3. 选择默认模型
4. 完成配置

**手动配置（可选）**：

编辑配置文件 `~/.openclaw/config.json`：

```json
{
  "models": {
    "providers": [
      {
        "providerId": "bailian",
        "apiKey": "你的API密钥",
        "models": [
          {
            "id": "qwen-plus",
            "primary": true
          }
        ]
      }
    ]
  }
}
```

---

## 📋 第4步：启动Gateway

```bash
# 启动OpenClaw Gateway
openclaw gateway start
```

✅ 成功标志：
```
[OpenClaw Gateway] Starting...
[OpenClaw Gateway] Listening on http://localhost:18789
[OpenClaw Gateway] Ready to receive connections
```

**提示**: Gateway需要在后台持续运行

---

## 📋 第5步：连接对话平台

### 方式1: Web聊天（最快）

访问 http://localhost:18789/chat 开始对话

### 方式2: 钉钉

```bash
# 配置钉钉集成
openclaw feishu init
```

按照提示扫描二维码或配置应用凭证

### 方式3: Telegram

```bash
# 配置Telegram Bot
openclaw telegram init
```

---

## ✅ 验证成功

发送测试消息：

**用户**: 你好！
**AI**: 你好！我是OpenClaw，有什么可以帮助你的吗？

🎉 **恭喜！你的AI助手已经就绪！**

---

## 🚀 下一步

- [ ] 查看更多[安装选项](../linux/linux-install-guide.md)
- [ ] 学习[API配置](../api-config/api-configuration.md)
- [ ] 选择合适的[模型](../api-config/model-comparison.md)
- [ ] 了解[成本优化](../api-config/cost-optimization.md)
- [ ] 部署到[云服务器](../cloud/cloud-deployment-guide.md)

---

## ❓ 常见问题

### Q: 免费额度能用多久？

**A:** 硅基流动的2000万Tokens足够新手使用1-3个月，具体取决于使用频率

### Q: 不想付费怎么办？

**A:** 先使用免费额度体验，觉得有价值再考虑订阅。硅基流动、火山引擎都有免费试用

### Q: 安装失败？

**A:** 确保：
- 已安装Node.js (v18+)
- 有网络连接
- 有写入权限

详细排查见[故障排除](../advanced/troubleshooting.md)

---

**创建时间**: 2026-02-22
**版本**: 1.0
**适用版本**: OpenClaw 2026.2.x
