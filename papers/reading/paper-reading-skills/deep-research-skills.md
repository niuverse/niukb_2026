# Deep Research Skills 调研报告

> 调研日期: 2026-02-24  
> 调研目标: 寻找类似 Deep Research 功能的 OpenClaw/Claude Skills  
> 重点关注: 自动化研究、多步骤推理、报告生成

---

## 什么是 Deep Research

**Deep Research** 是 AI Agent 领域的新兴范式，代表系统能够：
- 自主规划多步骤研究任务
- 调用多种工具（搜索、浏览、计算、分析）
- 生成结构化、引用充分的研究报告
- 处理复杂、开放性的研究问题

**典型代表**:
- **OpenAI Deep Research** (2025年2月)
- **Google Gemini Deep Research** (2025年)
- **GenSpark Deep Research** (2025年1月)

---

## 找到的类似 Skills

### 1. Research Assistant Skills

#### 1.1 arxiv-watcher
**来源**: openclaw/skills (Playbooks)  
**GitHub**: https://github.com/openclaw/skills

**功能**:
- 搜索 ArXiv 并生成可操作摘要
- 按关键词、作者、类别发现论文
- Deep dive 模式提取实验设置和关键图表
- 保存摘要到持久化研究日志

**与 Deep Research 的相似度**: ⭐⭐⭐ (3/5)
- ✅ 自动化论文发现
- ✅ 结构化摘要
- ⚠️ 限于 ArXiv 来源
- ❌ 无多步骤推理

**安装**:
```bash
npx playbooks add skill openclaw/skills --skill arxiv-watcher
```

---

#### 1.2 arxiv-reader
**来源**: openclaw/skills (agentskill.sh)  
**GitHub**: https://agentskill.sh/@openclaw/arxiv-reader

**功能**:
- 基于 LLM Agent 对 arXiv 论文分类与深度阅读
- 直接打印阅读笔记
- 支持指定 arXiv ID 或 URL

**与 Deep Research 的相似度**: ⭐⭐⭐ (3/5)
- ✅ 深度阅读单篇论文
- ✅ 结构化笔记
- ⚠️ 限于 ArXiv
- ❌ 无自主搜索规划

**安装**:
```bash
/learn @openclaw/arxiv-reader
```

---

#### 1.3 paper-craft-skills
**来源**: GitHub - zsyggg/paper-craft-skills  
**GitHub**: https://github.com/zsyggg/paper-craft-skills  
**Stars**: 11

**功能**:
- **paper-analyzer**: 将论文转为深度技术文章
  - 3种写作风格：academic、storytelling、concise
  - 公式解释：插入公式图片并分解符号
  - 代码分析：将论文概念与 GitHub 源码对齐
  
- **paper-comic**: 将论文转为教育漫画
  - 4种艺术风格

**与 Deep Research 的相似度**: ⭐⭐⭐⭐ (4/5)
- ✅ 深度内容分析
- ✅ 多模态输出（文章、漫画）
- ✅ 公式和代码理解
- ⚠️ 单篇论文处理
- ❌ 无自主多源搜索

**安装**:
```bash
npx skills add zsyggg/paper-craft-skills
```

---

### 2. Web Research Skills

#### 2.1 web-search-skill
**来源**: openclaw/skills

**功能**:
- 集成多种搜索引擎（Brave、Google、Bing）
- 网页内容提取和摘要
- 搜索结果结构化输出

**与 Deep Research 的相似度**: ⭐⭐ (2/5)
- ✅ 网络搜索
- ⚠️ 基础搜索功能
- ❌ 无多步骤推理
- ❌ 无报告生成

---

#### 2.2 browser-automation
**来源**: openclaw/skills

**功能**:
- 自动化浏览器操作
- 多页面信息收集
- 表单填写和数据提取

**与 Deep Research 的相似度**: ⭐⭐⭐ (3/5)
- ✅ 可访问任意网页
- ✅ 多页面导航
- ⚠️ 需人工规划步骤
- ❌ 无自主推理

---

### 3. Analysis Skills

#### 3.1 code-simplifier
**来源**: niuverse/skills

**功能**:
- 代码复杂度分析
- 重构建议
- 模式识别

**与 Deep Research 的相似度**: ⭐⭐ (2/5)
- ✅ 深度分析
- ⚠️ 限于代码领域

---

#### 3.2 python-architect
**来源**: niuverse/skills

**功能**:
- 项目结构分析
- 架构建议
- 最佳实践检查

**与 Deep Research 的相似度**: ⭐⭐ (2/5)
- ✅ 系统性分析
- ⚠️ 限于 Python 项目

---

### 4. 专门的 Research Skills

#### 4.1 research-pal
**来源**: 社区 skill (未验证)

**声称功能**:
- 多源信息收集
- 交叉验证
- 引用生成

**状态**: 需要进一步验证

---

#### 4.2 deep-researcher (概念)
**来源**: 学术论文

**论文**: "Scaling Deep Research via Reinforcement Learning" (EMNLP 2025)  
**arXiv**: https://aclanthology.org/2025.emnlp-main.22.pdf

**核心思想**:
- 首个端到端训练 LLM-based deep research agent 的框架
- 通过强化学习优化多步骤研究策略
- 奖励模型基于研究报告质量

**与 Deep Research 的相似度**: ⭐⭐⭐⭐⭐ (5/5)
- ✅ 完全自主研究
- ✅ 多步骤规划
- ✅ 强化学习优化
- ⚠️ 学术论文，非可用 skill

---

## 能力对比矩阵

| Skill | 自主规划 | 多源搜索 | 结构化输出 | 引用生成 | 多步骤推理 | 报告质量 |
|-------|----------|----------|------------|----------|------------|----------|
| **OpenAI Deep Research** | ✅ | ✅ | ✅ | ✅ | ✅ | ⭐⭐⭐⭐⭐ |
| **arxiv-watcher** | ⚠️ | ⚠️ | ✅ | ⚠️ | ❌ | ⭐⭐⭐ |
| **arxiv-reader** | ❌ | ❌ | ✅ | ⚠️ | ❌ | ⭐⭐⭐ |
| **paper-craft-skills** | ⚠️ | ❌ | ✅ | ⚠️ | ⚠️ | ⭐⭐⭐⭐ |
| **web-search-skill** | ❌ | ✅ | ⚠️ | ❌ | ❌ | ⭐⭐ |
| **browser-automation** | ❌ | ✅ | ⚠️ | ❌ | ⚠️ | ⭐⭐⭐ |

---

## 推荐组合方案

### 方案 A: 论文深度研究 (Paper-Focused)

```
arxiv-watcher (发现论文)
    ↓
paper-craft-skills (深度分析)
    ↓
mineru-pdf (解析公式图像)
    ↓
生成结构化报告
```

**适用场景**: 学术研究、文献综述

**安装**:
```bash
npx playbooks add skill openclaw/skills --skill arxiv-watcher
npx skills add zsyggg/paper-craft-skills
```

---

### 方案 B: 通用深度研究 (General Research)

```
web-search-skill (多源搜索)
    ↓
browser-automation (深入页面)
    ↓
code-simplifier/python-architect (专业分析)
    ↓
生成综合报告
```

**适用场景**: 技术调研、竞品分析

---

### 方案 C: 构建真正的 Deep Research Skill

基于现有 skills，可以构建一个更接近 OpenAI Deep Research 的 skill：

**核心组件**:
1. **规划模块**: 分解研究问题为子任务
2. **搜索模块**: 多源信息收集 (arxiv-watcher + web-search)
3. **分析模块**: 深度内容分析 (paper-craft + code-simplifier)
4. **合成模块**: 生成结构化报告
5. **验证模块**: 交叉验证信息来源

**伪代码**:
```python
class DeepResearchSkill:
    def research(self, query: str) -> ResearchReport:
        # 1. 规划
        plan = self.planner.create_plan(query)
        
        # 2. 多源搜索
        sources = []
        for subtask in plan.subtasks:
            if subtask.type == "academic":
                sources.extend(arxiv_watcher.search(subtask.query))
            else:
                sources.extend(web_search.search(subtask.query))
        
        # 3. 深度分析
        analyses = []
        for source in sources:
            if source.type == "paper":
                analyses.append(paper_craft.analyze(source))
            else:
                analyses.append(self.summarize(source))
        
        # 4. 合成报告
        report = self.synthesizer.generate(
            query=query,
            analyses=analyses,
            citations=sources
        )
        
        return report
```

---

## 缺失能力

当前 skills 生态中 **缺失** 的关键 Deep Research 能力：

1. **自主任务规划**
   - 将开放性问题分解为可执行步骤
   - 动态调整研究策略

2. **多步骤推理链**
   - 基于中间结果决定下一步行动
   - 处理依赖关系

3. **信息交叉验证**
   - 多源信息一致性检查
   - 可信度评估

4. **引用和溯源**
   - 自动生成规范引用
   - 支持追溯原始来源

5. **迭代优化**
   - 基于反馈改进搜索策略
   - 填补信息缺口

---

## 建议

### 短期 (使用现有 skills)

1. **论文研究**: arxiv-watcher + paper-craft-skills + mineru-pdf
2. **技术调研**: web-search-skill + browser-automation
3. **代码分析**: code-simplifier + python-architect

### 中期 (组合增强)

开发一个 **deep-research** skill，整合：
- 规划能力 (基于 LLM 的任务分解)
- 多源搜索 (arxiv + web + github)
- 专业分析 (paper + code + data)
- 报告生成 (结构化 markdown)

### 长期 (完整 Deep Research)

参考学术论文 "Scaling Deep Research via Reinforcement Learning"，实现：
- 端到端训练的研究 agent
- 强化学习优化研究策略
- 质量评估和迭代改进

---

## 参考资源

1. **OpenAI Deep Research**: https://openai.com/index/introducing-deep-research/
2. **GenSpark Deep Research**: https://www.genspark.ai/
3. **DeepResearcher Paper**: https://aclanthology.org/2025.emnlp-main.22.pdf
4. **Deep Research Survey**: https://arxiv.org/pdf/2506.12594

---

*调研完成时间: 2026-02-24*  
*建议定期更新，跟踪最新 skills 发展*
