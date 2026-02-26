# 🤖 每日AI工作流调研任务说明 | Daily AI Workflow Research Task

## 📋 任务详情 | Task Details

| 项目 | Item | 详情 | Details |
|-----|------|-----|---------|
| **任务名称** | Task Name | daily-ai-research | daily-ai-research |
| **执行时间** | Execution Time | 每天早上 10:00 (GMT+8) | Daily 10:00 AM (GMT+8) |
| **执行频率** | Frequency | 每日 | Daily |
| **目标仓库** | Target Repository | git@github.com:niuverse/niukb_2026.git | git@github.com:niuverse/niukb_2026.git |
| **输出语言** | Output Language | 中英双语 | Bilingual (CN/EN) |  

## 🎯 调研目标

搜索并总结关于以下主题的最新文章和实践：

1. **AI Coding Agent** - Codex, Claude Code, GitHub Copilot 等工具的新用法
2. **自动化工作流** - 如何通过AI自动化日常开发/工作流
3. **效率提升实践** - 实际案例和最佳实践
4. **工具集成** - 新工具、新插件、新workflow

## 📁 输出位置 | Output Locations

调研报告将保存到以下位置：

**主要报告（双语）| Main Report (Bilingual):**
```
ai-workflow-digest/YYYY-MM/daily-digest_YYYY-MM-DD.md
```

**简化版笔记 | Simplified Notes:**
```
notes/daily-ai-insights/YYYY-MM/daily-insights_YYYY-MM-DD.md
```

### 报告内容 | Report Content

- ✅ 中英双语标题和元数据 | Bilingual titles and metadata
- ✅ 英文原文 + 中文翻译 | English original + Chinese translation
- ✅ 双语表格和数据 | Bilingual tables and data
- ✅ 双语使用指南 | Bilingual usage guide

## ⚙️ 前置配置

### 1. 配置 Brave Search API Key (必需)

调研需要搜索功能，需要配置 Brave API Key：

```bash
# 获取 API Key: https://brave.com/search/api/
openclaw configure --section web
# 或设置环境变量
export BRAVE_API_KEY="your-api-key"
```

### 2. 配置 Git 身份

确保 cron 任务可以推送代码：

```bash
# 检查 Git 配置
git config --global user.name "niubot"
git config --global user.email "your-email@example.com"

# 确保有 SSH key 或 HTTPS 凭证
ssh-keygen -t ed25519 -C "your-email@example.com"
cat ~/.ssh/id_ed25519.pub
# 添加到 GitHub: Settings -> SSH and GPG keys -> New SSH key
```

## 🚀 手动触发

如需立即执行一次调研：

```bash
openclaw cron run daily-ai-research
```

## 📝 任务内容

Cron任务将执行以下操作：

1. 🔍 搜索今日AI工作流相关文章
2. 📖 阅读并筛选有价值的内容
3. 📝 总结核心观点和实践价值
4. 📤 生成Markdown报告
5. 💾 推送到 niukb_2026 仓库

## 📊 预期输出格式

```markdown
---
title: "AI 工作流自动化日报"
date: 2026-02-26
category: daily-insights
tags: [ai-automation, workflow, productivity]
---

# 🤖 AI 工作流自动化日报 - 2026-02-26

## 📌 今日精选

### 1. [文章标题]
**来源**: [来源网站]  
**链接**: [URL]

**核心观点**:
- 要点1
- 要点2

**实践价值**: ⭐⭐⭐⭐⭐

...
```

## 🔄 管理任务

```bash
# 查看所有定时任务
openclaw cron list

# 查看任务执行历史
openclaw cron runs daily-ai-research

# 禁用任务
openclaw cron disable daily-ai-research

# 启用任务
openclaw cron enable daily-ai-research

# 删除任务
openclaw cron rm daily-ai-research

# 编辑任务
openclaw cron edit daily-ai-research --cron "0 9 * * *"  # 改为9点
```

## ⚠️ 注意事项

1. **API Key**: 必须先配置 Brave Search API Key，否则搜索功能无法使用
2. **Git权限**: 确保OpenClaw运行的用户有权限推送到你的GitHub仓库
3. **网络**: 确保主机可以访问 Brave Search API 和 GitHub
4. **存储**: 每天生成一个新文件，长期运行会积累较多文件

## 📞 故障排查

### 问题: 搜索失败
**解决**: 检查 BRAVE_API_KEY 是否配置正确

### 问题: 推送失败
**解决**: 检查Git配置和SSH key权限

### 问题: 任务未执行
**解决**: 检查 cron scheduler 状态
```bash
openclaw cron status
```

## 🎉 开始享受自动化！

配置完成后，每天早上10点都会有一份新鲜的AI工作流洞察报告自动推送至你的知识库。

---
*配置时间: 2026-02-26*  
*配置者: 牛宝 (niubot)*
