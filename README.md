# WeChat Article Generator Skills v1.1

面向微信公众号的中文长文写作 Skill。

## v1.1 重点升级

这次不再把“完整介绍素材”作为最高目标，而把：

> **文章主线、作者判断、信息增量、手机阅读体验**

放到更高优先级。

核心变化：

1. 从“README 翻译”升级为“研究后写判断”；
2. 开头要求 30 秒内进入核心；
3. 文章核心点默认只选 3–5 个；
4. 正文一级标题建议 18 px，二级标题 16 px；
5. 正文不再滥用超大标题；
6. 互动话题、点赞、在看、信息表格全部从“强制”改为“按需”；
7. 删除“多素材绝不合并”的硬规则，改为用户意图优先；
8. 加入微信公众号推荐运营规范自检；
9. 加入“事实 / 项目自述 / 作者判断 / 延伸分析”的边界；
10. GitHub 和论文模式都要求优先寻找源码、正文、Benchmark 中的真正信息增量。

## 文件结构

```text
wechat-article-generator-skills-v1.1/
├── SKILL.md
├── README.md
├── CHANGELOG.md
├── single-file-prompt.md
├── references/
│   ├── core-writing-rules.md
│   ├── article-structures.md
│   ├── title-patterns.md
│   ├── avoid-list.md
│   ├── research-playbook.md
│   ├── wechat-editor-style.md
│   ├── recommendation-compliance.md
│   └── editorial-quality-gate.md
├── modes/
│   ├── github-project.md
│   ├── research-paper.md
│   ├── news-event.md
│   ├── twitter-post.md
│   ├── product-review.md
│   ├── tutorial-guide.md
│   ├── opinion-essay.md
│   ├── freebie-deal.md
│   └── general.md
└── examples/
    ├── github-article-outline.md
    └── paper-article-outline.md
```

## 推荐使用方法

Claude Code / Codex / Cursor 等支持 Skills 的工具，可直接加载整个目录。

普通聊天模型可使用 `single-file-prompt.md`。

## 版本说明

GitHub 当前主分支里的旧 Skill 自身标注过 `2.0.0`。本包按照用户自己的产品版本命名要求，发布为 **v1.1**。若未来直接合并回原仓库，建议统一一次版本号，避免 `1.1` 与仓库现有 `2.0.0` 语义冲突。
