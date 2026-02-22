# 内容分发使用指南

> 如何使用自动分发工具将教程内容发布到各大平台

---

## 🚀 快速开始

### 方法1: 使用 GitHub Actions（推荐）

1. **手动触发分发**

   进入 GitHub 仓库 → Actions → "内容分发" → "Run workflow" → 选择平台

2. **自动触发分发**

   每次推送到 main 分支时自动运行（当前未启用，需修改 workflow）

---

### 方法2: 本地运行

```bash
# 进入项目目录
cd OpenClaw-Guide-for-Beginners

# 运行分发脚本
python3 scripts/distribute/distribute.py [平台]
```

**可用命令**:

```bash
# 分发到所有平台
python3 scripts/distribute/distribute.py all

# 分发到知乎
python3 scripts/distribute/distribute.py zhihu

# 分发到小红书
python3 scripts/distribute/distribute.py xiaohongshu

# 分发到微信公众号
python3 scripts/distribute/distribute.py wechat

# 分发到掘金
python3 scripts/distribute/distribute.py juejin
```

---

## 📂 输出目录结构

```
dist/
├── zhihu/              # 知乎版本
│   ├── README.md
│   └── docs/
├── xiaohongshu/        # 小红书版本
│   ├── README.md
│   └── docs/
├── wechat/             # 公众号版本
│   ├── README.md
│   └── docs/
├── juejin/             # 掘金版本
│   ├── README.md
│   └── docs
└── distribution-report.json  # 分发报告
```

---

## 📊 分发报告

每次分发后会生成 `dist/distribution-report.json` 报告：

```json
{
  "timestamp": "2026-02-22T19:12:00",
  "author": "junhang lai",
  "platforms": {
    "zhihu": {
      "name": "知乎",
      "file_count": 15,
      "output_dir": "/path/to/dist/zhihu"
    },
    "xiaohongshu": {
      "name": "小红书",
      "file_count": 15,
      "output_dir": "/path/to/dist/xiaohongshu"
    }
  },
  "total_files": 60
}
```

---

## 🔧 平台适配说明

### 知乎

**适配特点**:
- 保留完整 Markdown 格式
- 添加原文链接和作者信息
- 添加同步状态标识

**发布步骤**:
1. 复制 `dist/zhihu/` 中的内容
2. 粘贴到知乎编辑器
3. 检查格式是否正确
4. 添加标签（OpenClaw, AI, 开发工具）
5. 发布

---

### 小红书

**适配特点**:
- 提取关键步骤（30行以内）
- 添加 emoji 和视觉元素
- 添加完整教程链接
- 适合快速浏览

**发布步骤**:
1. 查看 `dist/xiaohongshu/` 中的内容
2. 根据内容制作配图（4-9张）
3. 复制文本到小红书编辑器
4. 添加话题标签（#OpenClaw #AI工具 #程序员）
5. 发布

---

### 微信公众号

**适配特点**:
- 添加引导关注语
- 添加原文链接
- 格式适合阅读
- 适合深度内容

**发布步骤**:
1. 复制 `dist/wechat/` 中的内容
2. 粘贴到公众号编辑器
3. 添加封面图
4. 预览检查格式
5. 发布

---

### 掘金

**适配特点**:
- 保留完整 Markdown
- 添加标签
- 添加作者信息
- 适合技术分享

**发布步骤**:
1. 复制 `dist/juejin/` 中的内容
2. 粘贴到掘金编辑器
3. 添加标签和分类
4. 添加相关文章链接
5. 发布

---

## 🎯 发布建议

### 发布频率

| 平台 | 建议频率 | 最佳时间 |
|------|---------|---------|
| 知乎 | 每周1篇 | 工作日 18:00-20:00 |
| 小红书 | 每周2篇 | 周末 10:00-12:00 |
| 公众号 | 每月2篇 | 周二/周四 20:00 |
| 掘金 | 每周1篇 | 工作日 12:00-14:00 |

### 内容优先级

**高优先级**（核心内容）:
- ✅ 快速开始指南
- ✅ Docker 部署教程
- ✅ API 配置指南
- ✅ 模型选择指南

**中优先级**（补充内容）:
- ✅ 云服务器部署
- ✅ 平台对接教程
- ✅ 成本优化指南

**低优先级**（高级内容）:
- ✅ WSL 配置
- ✅ Docker 高级配置
- ✅ 故障排除

---

## 🔗 完整工作流

### 1. 准备内容

```bash
# 确保本地内容是最新的
git pull origin main
```

### 2. 生成平台版本

```bash
# 生成所有平台版本
python3 scripts/distribute/distribute.py all

# 或使用 GitHub Actions 手动触发
```

### 3. 审核内容

```bash
# 查看生成的文件
ls -la dist/zhihu/
cat dist/zhihu/README.md
```

### 4. 手动调整（可选）

根据平台特点手动调整：
- 小红书：添加配图
- 公众号：调整排版
- 知乎：添加相关链接

### 5. 发布到平台

按照各平台的发布步骤操作

### 6. 记录发布状态

在 `dist/published-logs.md` 记录：
```markdown
## 2026-02-22

- 知乎: OpenClaw 快速开始指南 ✅
- 小红书: Docker 部署教程 ⏳ 待发布
- 公众号: API 配置指南 ✅
```

---

## 🛠️ 自定义适配

如果需要自定义某个平台的适配逻辑，编辑 `scripts/distribute/distribute.py`：

```python
def format_for_custom_platform(content, metadata):
    """自定义平台格式化"""
    # 添加你的自定义逻辑
    return customized_content
```

然后在 `PLATFORMS` 字典中添加新平台：

```python
PLATFORMS = {
    # ... 其他平台
    "custom": {
        "name": "自定义平台",
        "output_dir": DIST_DIR / "custom",
        "formatter": "format_for_custom_platform"
    }
}
```

---

## 📚 相关文档

- [分发策略](DISTRIBUTION-STRATEGY.md) - 完整的分发策略和规划
- [作者信息](AUTHORS.md) - 作者信息和贡献指南
- [GitHub Actions 文档](https://docs.github.com/en/actions)

---

**创建时间**: 2026-02-22
**作者**: junhang lai
**最后更新**: 2026-02-22
