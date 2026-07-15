# 更新日志

本项目遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [0.2.0] - 2026-07-15

新增定时任务交付模板，让 agent 跑完研究后能把速报作为文件发给用户。

### 新增

- **交付模板**：`templates/digest.md.template`（频道推送 Markdown 消息）与 `templates/digest.html.template`（可视化 HTML 报告）。
- **交付工作流**：SKILL.md 新增「Deliver output via templates」章节，定义占位符填写规则、文件命名（`digest-<period-key>.{md,html}`）与覆盖刷新策略。
- **模板设计**：HTML 报告采用楷体优先、柔和留白与流动渐变，适合浏览器阅读或打印为 PDF。
- **交付与存储解耦**：交付速报不依赖 Mneme 写入批准，可在用户批准 wiki 写入前先发出文件。

### 变更

- README 中英文徽章、下载链接、项目档案树更新到 0.2.0。

## [0.1.0] - 2026-07-15

首个公开版本。

### 新增

- **AI 新闻研究工作流**：覆盖解析请求、研究、筛选去重、报告、Mneme 存储五个阶段。
- **可配置的定时任务**：支持按报告周期、时区、条目数确定性运行，幂等防重。
- **质量评分体系**：`references/quality-rubric.md` 提供证据、实质、影响、新颖性、独立佐证与推广风险六个维度。
- **公开信源路由图**：`references/sources.md` 覆盖官方实验室、论文、开源、独立报道、中文媒体与政策治理。
- **Mneme 存储契约**：`references/mneme-storage.md` 定义事件页、摘要页、原始论文 PDF 的页面模型与去重规则。
- **预览再写入**：所有 wiki 写入前必须通过只读审计并向用户展示完整变更预览，经显式批准后才落盘。
- **Agent 接口定义**：`agents/openai.yaml` 提供 OpenAI 兼容 Agent 的展示名与默认提示。
- **skills.sh 发布格式**：技能包位于 `skills/ai-news/`，可通过 `npx skills add` 一键安装。

[0.1.0]: https://github.com/Scott1743/ai-news/releases/tag/v0.1.0
[0.2.0]: https://github.com/Scott1743/ai-news/releases/tag/v0.2.0
