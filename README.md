<div align="center">

#  AI 新闻雷达

**一个面向事实核验与 Mneme 知识库归档的 AI 新闻研究 Agent Skill**

*今日的 AI 大事件，今晚就归档进你的知识库。*

[![MIT License](https://img.shields.io/badge/license-MIT-purple.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-0.2.0-pink.svg)](CHANGELOG.md)
[![Skills.sh](https://img.shields.io/badge/skills.sh-available-blue.svg)](https://www.skills.sh/?q=ai-news)

</div>

[English](README.en.md) | 简体中文 | [📖 介绍页](https://scott1743.github.io/ai-news/)

---

## ✨ 为什么选择 AI 新闻雷达？

AI 圈每天信息过载，标题党、SEO 改写、厂商软文混在一起。你需要的不只是"看到新闻"，而是一套能打开原始页面、核实来源、打分筛选、去重归档的研究流程。

**AI 新闻雷达** 不是聚合器，而是一个严谨的研究员：

- 它不会把搜索摘要当成证据
- 它不会把厂商通稿当成独立报道
- 它只是用可追溯的方法，帮你把真正重要的 AI 事件沉淀进知识库

---

## 📡 核心功能

### 源头核验
优先打开一手信源——官方公告、论文 PDF、代码仓库、监管文件。永远不把搜索结果摘要、社交帖子或聚合器摘要当作证据。

### 质量评分
每个候选条目按证据、实质、影响、新颖性、独立佐证五个正向维度打分，再扣除推广风险。硬性排除赞助内容、内容农场改写和无原始来源的指控。

### 事件去重
按真实事件聚类，而非按标题。同一个模型发布被十家媒体报道只算一条，主链接保留一手公告，有用的独立报道放进引用。

### Mneme 归档
以 Mneme OKF Markdown 作为唯一持久存储。事件页、摘要页、原始论文 PDF 各司其职，按报告周期生成稳定 key，不建第二个摘要。

### 定时交付模板
用户多在定时任务里使用。agent 跑完研究后填入 `templates/` 下的 Markdown 消息模板与 HTML 报告模板，把文件发给用户——速报可直接推送到频道，也可在浏览器阅读或打印。交付与 Mneme 写入解耦，不必等批准就能先收到速报。

### 预览再写入
所有知识库写入前必须跑只读审计，向用户展示完整变更预览——包含路径、frontmatter、标签、链接、日志条目。经显式批准后才落盘。

### 安全边界
不绕过登录墙和付费墙；区分发布时间与事件时间；意见和预测与事实分开标注；无法核实的日期标记为未知并通常排除。

---

## 📦 快速开始

### 方式一：通过 skills.sh 安装（推荐）
```bash
npx skills add Scott1743/ai-news/skills/ai-news
```

### 方式二：手动安装

1. 下载最新版本：[ai-news-0.2.0.zip](https://github.com/Scott1743/ai-news/releases/download/v0.2.0/ai-news-0.2.0.zip)
2. 解压到你的 Agent skills 目录
3. 重启对应的 Agent 客户端加载技能

---

## 🌱 使用示例

```
帮我查今天的 AI 新闻
```
> 默认覆盖最近 24 小时，按事件类别分组，5–10 条精选。

```
最近一周大模型有什么更新
```
> 自定义时间窗口与主题，质量评分附在每条之后。

```
把这批 AI 新闻存进 Mneme
```
> 先展示完整变更预览，批准后按 Mneme dream 工作流写入事件页与摘要页。

```
每天早上九点整理一次 AI 新闻
```
> 经确认后注册定时任务，写入确定性的周期、时区、条目数与覆盖窗口。

---

## 📝 版本历程

0.1.0 的首个公开版本，确立了五阶段工作流（解析请求、研究、筛选去重、报告、Mneme 存储）与"预览再写入"契约。0.2.0 新增定时任务交付模板：agent 跑完研究后填入 `templates/` 下的 Markdown 消息模板与 HTML 报告模板，把文件发给用户，让每日速报可直接推送到频道或浏览器阅读。依赖已安装的 [Mneme](https://github.com/Scott1743/mneme) 技能提供知识库与只读审计；本技能不复制或重新实现 Mneme，只通过其公开的 dream 工作流协作。

---

## 📚 项目档案

```
ai-news/
└── skills/
    └── ai-news/
        ├── SKILL.md              # Agent Skill 主入口与工作流定义
        ├── agents/
        │   └── openai.yaml       # OpenAI 兼容 Agent 接口配置
        ├── templates/            # 定时任务交付模板
        │   ├── digest.md.template   # 频道推送 Markdown 消息模板
        │   └── digest.html.template # 可视化 HTML 报告模板
        └── references/
            ├── sources.md        # 公开信源路由图
            ├── quality-rubric.md # 质量评分体系
            └── mneme-storage.md  # Mneme 存储契约
```

---

## 📖 延伸阅读

- [SKILL 工作流定义](skills/ai-news/SKILL.md)
- [公开信源路由图](skills/ai-news/references/sources.md)
- [质量评分体系](skills/ai-news/references/quality-rubric.md)
- [Mneme 存储契约](skills/ai-news/references/mneme-storage.md)
- [更新日志](CHANGELOG.md)

---

## 📜 设计原则

- **一手证据优先**：官方公告、论文、代码、监管文件优先于二手报道。
- **可追溯**：保留规范 URL、署名作者、精确发布时间与原始时间文本。
- **不自动写入**：研究请求不等于知识库写入授权，必须逐次预览批准。
- **不绕过访问控制**：登录墙与付费墙不可绕过，无公开一手来源则略过。
- **不制造数据**：无法核实的日期、引用、佐证一律标记未知，不用模型记忆冒充当前新闻。

---

## 📜 版权

本项目采用 [MIT License](LICENSE) 开源。

<div align="center">

*愿你每天的重要 AI 资讯，都被妥善核验与归档。*

</div>
