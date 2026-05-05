# 🐳 ClawDock 官方部署指南

> OpenClaw 官方 Docker 镜像，开箱即用，包含所有依赖和预配置环境。

---

## 📋 什么是 ClawDock

ClawDock 是 OpenClaw 官方提供的 Docker 镜像，包含：
- ✅ 最新稳定版 OpenClaw
- ✅ 所有运行时依赖（Node.js 24 LTS、Python 3.11等）
- ✅ 预配置的插件和扩展
- ✅ 自动健康检查
- ✅ 优化的启动参数
- ✅ 开箱即用的体验

**推荐所有用户优先使用 ClawDock 部署 OpenClaw**。

---

## 🚀 前置条件

- Docker 20.10+（推荐 24.0+）
- 至少 1GB 内存
- 至少 2GB 磁盘空间
- 18789 端口未被占用

---

## ⚡ 快速部署（推荐）

### 方式一：一键脚本部署（最简单）

```bash
# 下载部署脚本
curl -O https://raw.githubusercontent.com/bitroboticslab/OpenClaw-Guide-for-Beginners/main/scripts/install-docker.sh

# 添加执行权限
chmod +x install-docker.sh

# 运行脚本
./install-docker.sh
```

脚本会自动完成：
1. 检查 Docker 环境
2. 拉取最新 ClawDock 镜像
3. 引导配置 API Key
4. 启动容器并配置开机自启
5. 显示访问地址和管理命令

---

### 方式二：手动部署

#### 步骤1：创建数据目录

```bash
mkdir -p openclaw/data
cd openclaw
```

#### 步骤2：创建配置文件（可选）

如果需要提前配置 API Key，可以创建 `openclaw.json` 文件：
```json
{
  "models": {
    "providers": {
      "siliconflow": {
        "baseUrl": "https://api.siliconflow.cn/v1",
        "apiKey": "你的硅基流动API Key",
        "api": "openai-completions"
      }
    }
  },
  "agents": {
    "defaults": {
      "model": {
        "primary": "siliconflow/Pro/MiniMaxAI/MiniMax-M2.5"
      }
    }
  }
}
```

> 也可以省略此步骤，启动后在 Web 控制台配置。

#### 步骤3：启动容器

```bash
docker run -d \
  --name openclaw \
  --restart unless-stopped \
  -p 18789:18789 \
  -v $(pwd)/openclaw.json:/root/.openclaw/openclaw.json:ro \
  -v $(pwd)/data:/root/.openclaw/data \
  openclaw/clawdock:latest
```

#### 步骤4：验证部署

等待约10秒，访问 `http://你的服务器IP:18789`，如果能看到 OpenClaw 控制台则部署成功。

---

## 🐙 Docker Compose 部署（推荐生产环境）

### 步骤1：创建 `docker-compose.yml` 文件

```yaml
version: '3.8'

services:
  openclaw:
    image: openclaw/clawdock:latest
    container_name: openclaw
    restart: unless-stopped
    ports:
      - "18789:18789"
    volumes:
      - ./openclaw.json:/root/.openclaw/openclaw.json:ro
      - ./data:/root/.openclaw/data
    environment:
      - TZ=Asia/Shanghai
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:18789/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 10s
```

### 步骤2：启动服务

```bash
docker compose up -d
```

### 步骤3：查看状态

```bash
docker compose ps
```

---

## 📖 配置说明

### 端口映射
- `18789:18789`：Web 控制台和 API 服务端口，如果需要修改，可以改为 `8080:18789` 等自定义端口。

### 数据持久化
- `/root/.openclaw/data`：所有数据（配置、插件、会话记录等）存储目录，必须持久化，否则容器删除后数据会丢失。
- `/root/.openclaw/openclaw.json`：主配置文件，只读挂载，修改后需要重启容器生效。

### 环境变量
- `TZ=Asia/Shanghai`：设置时区为中国标准时间，可根据需要调整为其他时区。

---

## 🔧 管理命令

| 操作 | 命令 |
|------|------|
| 查看状态 | `docker ps` |
| 查看日志 | `docker logs -f openclaw` |
| 停止容器 | `docker stop openclaw` |
| 启动容器 | `docker start openclaw` |
| 重启容器 | `docker restart openclaw` |
| 进入容器 | `docker exec -it openclaw bash` |
| 查看版本 | `docker exec openclaw openclaw --version` |
| 更新镜像 | `docker pull openclaw/clawdock:latest && docker restart openclaw` |
| 删除容器 | `docker rm -f openclaw` |

---

## ❓ 常见问题

### Q: 无法访问控制台？
A: 检查以下几点：
1. 容器是否正常运行：`docker ps | grep openclaw`
2. 端口是否开放：云服务器安全组是否开放 18789 端口
3. 防火墙是否放行：`ufw allow 18789`（Ubuntu）或 `firewall-cmd --add-port=18789/tcp --permanent`（CentOS）
4. 查看容器日志：`docker logs openclaw` 检查是否有错误信息

### Q: 如何更新到最新版本？
A: 执行更新命令即可：
```bash
docker pull openclaw/clawdock:latest
docker restart openclaw
```

### Q: 数据会丢失吗？
A: 只要 `data` 目录被正确挂载，容器删除或重建都不会丢失数据。建议定期备份 `data` 目录。

### Q: 如何修改配置？
A: 修改宿主机上的 `openclaw.json` 文件，然后重启容器即可：
```bash
docker restart openclaw
```

### Q: 可以部署多个实例吗？
A: 可以，需要修改容器名称和端口映射：
```bash
docker run -d \
  --name openclaw2 \
  --restart unless-stopped \
  -p 18790:18789 \
  -v $(pwd)/openclaw2.json:/root/.openclaw/openclaw.json:ro \
  -v $(pwd)/data2:/root/.openclaw/data \
  openclaw/clawdock:latest
```

---

## 📞 帮助支持

如果遇到问题：
1. 查看 [Docker 故障排除指南](./docker-troubleshooting.md)
2. 访问官方文档：https://docs.openclaw.ai
3. 加入 Discord 社区：https://discord.com/invite/clawd
4. 在 GitHub 提交 Issue：https://github.com/openclaw/openclaw/issues

---

**最后更新**: 2026-05-05
**版本**: 1.0
