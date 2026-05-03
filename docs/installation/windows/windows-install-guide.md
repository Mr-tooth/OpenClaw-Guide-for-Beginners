<!-- This file is part of OpenClaw Guide for Beginners. Licensed under the MIT License. See LICENSE file for details. -->

# Windows 安装指南

> ⚠️ **重要提示**：本教程适用于有经验的Windows用户，**新手优先推荐使用WSL（Windows子系统Linux）安装**，稳定性和兼容性更好，后续维护更方便，是Windows平台的首选安装方式。
>
> 👉 [点击跳转到WSL安装教程](../wsl/wsl-setup.md)
>
> 本教程适用于 Windows 10/11 用户，从零开始完成 OpenClaw 的安装和配置

## 🎯 安装方式选择（按推荐度排序）

| 安装方式 | 推荐人群 | 难度 | 稳定性 | 特点 |
|----------|----------|------|--------|------|
| 🚀 **WSL2 安装** | 所有用户（官方推荐） | ⭐⭐ | ⭐⭐⭐⭐⭐ | 完整Linux环境，兼容性最好，无依赖冲突，性能接近原生Linux |
| 📦 **一键部署包** | 完全新手、不想用命令行 | ⭐ | ⭐⭐⭐⭐ | 双击安装，无需配置环境，自带所有依赖，适合快速体验 |
| ⚙️ **原生PowerShell安装** | 高级用户、熟悉Windows环境 | ⭐⭐⭐ | ⭐⭐⭐ | 直接在Windows系统运行，适合特殊场景需求 |

---

## 📋 前置要求

- Windows 10 2004+ 或 Windows 11
- 管理员权限
- 稳定的网络连接
- 至少4GB可用磁盘空间

---

## 📦 方式一：一键部署包安装（完全新手首选）

无需配置任何环境，双击即可完成安装，5分钟快速体验：

1. **下载部署包**
   - 访问官方下载页：https://openclaw.ai/download
   - 下载最新版 Windows 一键部署包（约50MB）
   - 或使用社区镜像：[华为云镜像](https://developer.huawei.com/consumer/cn/forum/topic/0207212065009865273)

2. **解压文件**
   - 右键下载的zip包，推荐使用 **WinRAR/7-Zip** 解压（避免系统自带解压工具损坏文件）
   - ⚠️ **重要**：解压路径必须是**纯英文、无空格、无特殊字符**，例如 `D:\OpenClaw`，不要放在 `D:\软件\OpenClaw` 这种含中文的路径

3. **安装运行**
   - 打开解压后的文件夹，双击 `OpenClaw 一键启动.exe`（红色龙虾图标）
   - 若弹出「Windows 已保护你的电脑」SmartScreen 拦截，点击「更多信息」→「仍要运行」
   - 选择安装路径（保持纯英文），点击「开始安装」
   - 等待1-3分钟初始化，首次启动会自动配置所有依赖

4. **验证成功**
   - 界面右上角显示「Gateway 在线」即安装成功
   - 自动打开Web管理界面：http://localhost:18789
   - 后续可直接通过桌面快捷方式启动

---

## 🔧 方式二：WSL2 安装（官方推荐，稳定性最好）

WSL2 是官方唯一推荐的Windows平台运行方案，兼容性最好、性能最优、无依赖冲突，适合所有用户（包括新手）。

👉 **完整安装配置教程请移步 [WSL 专属安装文档](../wsl/wsl-setup.md)**，一站式包含：
- WSL2 一键启用与Ubuntu系统安装
- WSL 性能调优与系统配置优化
- OpenClaw 部署、自动启动配置
- WSL与Windows网络互通方案
- 桌面快捷方式、文件共享等集成技巧
- 所有常见问题的解决方案

---

## ⚙️ 方式三：原生PowerShell安装（高级用户）

### 第一步：安装 Node.js
OpenClaw 需要 Node.js 24+ 版本。
### 方法一：使用 nvm 安装（推荐）
1. 下载 nvm-windows 安装包
   - 访问 [nvm-windows Releases](https://github.com/coreybutler/nvm-windows/releases)
   - 下载最新的 `nvm-setup.exe`
2. 以管理员身份运行安装程序
3. 打开 PowerShell（管理员模式），执行以下命令：
```powershell
# 安装 Node.js 24
nvm install 24
# 切换到 Node.js 24
nvm use 24
# 验证安装
node -v
# 应显示 v24.x.x
```
### 方法二：直接安装 Node.js
1. 访问 [Node.js 官网](https://nodejs.org/)
2. 下载 LTS 版本（24.x）
3. 运行安装程序，一路 Next
4. 重启 PowerShell 后验证：
```powershell
node -v
```


## 📥 第二步：安装 OpenClaw

### 一键安装（推荐）

打开 PowerShell（管理员模式），执行：

```powershell
# 运行官方安装脚本
iwr -useb https://openclaw.ai/install.ps1 | iex
```

安装过程约 2-5 分钟，会自动完成：
- 检测并安装依赖
- 下载 OpenClaw 核心文件
- 配置环境变量

### 手动安装

如遇网络问题，可以手动安装：

```powershell
# 克隆仓库
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 安装依赖
npm install

# 构建项目
npm run build
```

## ⚙️ 第三步：配置 API

OpenClaw 需要配置大模型 API 才能运行。推荐以下平台：

### 推荐一：硅基流动（新手推荐）

**优势**：注册送 2000万 Tokens，邀请双方各得代金券

1. 访问 [硅基流动官网](https://cloud.siliconflow.cn/i/lva59yow) 注册账号
2. 进入「模型广场」，选择想要使用的模型
3. 点击右上角头像 → 「API 密钥」→「创建新密钥」
4. 复制 API Key

**配置 OpenClaw：**

```bash
# 启动配置向导
openclaw onboard --install-daemon

# 选择模型提供商时选择 SiliconFlow
# 粘贴刚才复制的 API Key
```

### 推荐二：阿里百炼

**优势**：新人免费额度，Coding Plan 套餐性价比高

1. 访问 [阿里云百炼](https://bailian.console.aliyun.com) 开通服务
2. 开通新人免费额度
3. 获取 API Key：控制台 → API-KEY 管理 → 创建 API Key
4. 参考 [百炼官方文档](https://help.aliyun.com/zh/model-studio/openclaw) 配置 OpenClaw

### 推荐三：火山方舟 Coding Plan

**优势**：Lite 套餐首月仅 8.91 元，支持多款顶级模型

1. 访问 [火山方舟 Coding Plan](https://volcengine.com/L/oqijuWrltl0/  )
2. 选择套餐（Lite/Pro），使用邀请码可享 9 折
3. 获取 API Key
4. 配置 OpenClaw

> 💡 **提示**：Coding Plan 支持 Doubao、GLM、DeepSeek、Kimi 等多款模型，一个订阅多模型可用！

## 📱 第四步：配置消息平台（可选）

OpenClaw 支持多种消息平台，推荐新手从飞书开始：

### 飞书配置（一键安装，官方推荐）✨

最新版OpenClaw支持飞书官方一键安装脚本，无需手动创建应用和配置权限，扫码即可完成对接：

**前置要求**：OpenClaw 版本 >= 2026.3.2
```powershell
# 检查版本
openclaw -v

# 如果版本过低，先升级
npm install -g openclaw

# 执行飞书官方一键安装脚本
npx -y https://sf3-cn.feishucdn.com/obj/open-platform-opendoc/8ab6e7a04c17db1becfcbda8ca35f091_1rCCFRWlRV.tgz install
```

执行过程中会弹出二维码，用飞书客户端扫码即可一键创建飞书机器人，自动完成所有配置。

> 👉 查看[飞书官方详细教程](http://feishu.cn/content/article/7613711414611463386)
>
> 详细的飞书手动对接教程请参考 [飞书对接文档](../integration/feishu-integration.md)

<details>
<summary><b>手动配置飞书（不推荐，适合需要自定义的用户）</b></summary>

### 手动配置步骤

1. 创建飞书开发者账号
   - 访问 [飞书开放平台](https://open.feishu.cn)
   - 创建企业自建应用

2. 配置应用权限
   - 进入「权限管理」
   - 添加以下权限：
     - `im:message` - 获取与发送消息
     - `im:message:send_as_bot` - 以应用身份发消息

3. 获取凭证
   - 复制 App ID 和 App Secret

4. 配置 OpenClaw
```bash
openclaw onboard --install-daemon
# 选择 Feishu (Lark Open Platform)
# 输入 App ID 和 App Secret
```

</details>

## ✅ 第五步：启动服务

```bash
# 启动 OpenClaw
openclaw gateway start

# 查看状态
openclaw status

# 查看日志
openclaw logs
```

启动成功后，你可以：
- 访问 Web 界面：http://localhost:3000
- 通过配置的消息平台与 AI 对话

## 🔍 常见问题排查（Windows专属）

### 问题1：`node` / `openclaw` 命令不存在
**解决方案**：
- 确认 Node.js 安装成功，版本 >=24
- 重启 PowerShell 或重启电脑
- 检查系统环境变量是否包含 Node.js 和 npm 全局路径
- 原生安装可执行 `npm config get prefix` 查看全局安装路径，手动加入系统PATH

### 问题2：安装脚本下载失败 / 网络超时
**解决方案**：
- 检查网络连接，尝试关闭代理后重试
- 手动下载安装脚本到本地执行
- 使用国内镜像源：`npm config set registry https://registry.npmmirror.com`
- WSL2用户可配置WSL代理共享Windows主机代理

### 问题3：API 连接失败 / 模型无响应
**解决方案**：
- 检查 API Key 是否正确，没有多余空格
- 确认账户余额充足，模型有权限访问
- 检查Windows防火墙是否阻止OpenClaw访问网络
- 国内用户可配置API代理或使用国内模型提供商（硅基流动、火山方舟等）

### 问题4：权限不足 / EACCES 错误
**解决方案**：
- 以管理员身份运行 PowerShell / 一键启动程序
- 右键程序 → 「属性」→「兼容性」→ 勾选「以管理员身份运行此程序」
- WSL2用户不要使用sudo运行npm安装，会导致权限混乱

### 问题5：SmartScreen 拦截安装程序
**解决方案**：
- 点击弹窗下方的「更多信息」
- 点击右下角的「仍要运行」即可，程序是安全开源的，可放心使用
- 若仍被拦截，可在Windows安全中心 → 「病毒和威胁防护」→ 「保护历史记录」中允许该程序

### 问题6：路径含中文导致启动失败
**解决方案**：
- OpenClaw不支持中文、空格、特殊字符的安装路径
- 将程序移动到纯英文路径，例如 `C:\OpenClaw` 或 `D:\Tools\OpenClaw`
- 检查Windows用户名是否为中文，若是建议在WSL2中安装避开此问题

### 问题7：WSL2 无法访问Web界面
**解决方案**：
- 在WSL终端执行 `ip addr show eth0` 查看WSL的IP地址
- 使用 `http://<WSL_IP>:18789` 访问，而不是127.0.0.1
- 若仍无法访问，检查WSL防火墙设置：`sudo ufw allow 18789`

### 问题8：重启电脑后服务不自动启动
**解决方案**：
- 一键部署包用户：在设置中勾选「开机自动启动」
- WSL2用户：配置systemd服务 `systemctl --user enable --now openclaw-gateway`
- 原生安装用户：添加启动脚本到Windows「启动」文件夹或创建计划任务

## 📚 进阶阅读

- [API 配置详解](../configuration/api-configuration.md)
- [平台对接教程](../integration/README.md)
- [进阶配置优化](../advanced/README.md)

---

## 💰 优惠链接汇总

| 平台 | 链接 | 优惠说明 |
|------|------|----------|
| 硅基流动 | [注册链接](https://cloud.siliconflow.cn/i/lva59yow) | 注册送 2000万 Tokens |
| 阿里百炼 | [开通链接](https://bailian.console.aliyun.com) | 新人免费额度 |
| 火山方舟 | [Coding Plan](https://volcengine.com/L/oqijuWrltl0/  ) | 首月 8.91 元起 |
| 智谱 GLM | [订阅链接](https://www.bigmodel.cn/glm-coding?ic=BUDVTRHUYH) | 年付优惠 |

> 通过以上链接注册可享受额外优惠，同时支持作者持续更新教程 ❤️

---

**上一页**：[返回首页](../../README.md) | **下一页**：[macOS 安装指南](../macos/README.md)

<!-- This file is part of OpenClaw Guide for Beginners. Licensed under the MIT License. See LICENSE file for details. -->
