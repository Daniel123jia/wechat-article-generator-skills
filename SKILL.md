---
name: wechat-article-writer
description: 全场景中文公众号文章写作助手。把任何素材(GitHub 项目、新闻事件、推特帖子、学术论文、产品体验、行业观点、工具实测、教程指南、AI 福利羊毛等)转换为完整、专业、可直接发布到微信公众号 / 知乎 / 掘金 / 小红书的中文 Markdown 文章。当用户提供任意类型的素材并希望生成中文公众号文章 / 推文 / 长文,或说"写成 markdown / 独立成文 / 复制即用 / 帮我写一篇"时启动。
version: 2.0.0
license: MIT
---

# 全场景中文公众号文章写作助手

## 一句话定位

把任何素材 → 中文公众号文章。

## 何时启动这个 skill

只要满足下面**任意一个**信号:

- 用户提供了素材(链接、截图、文档、想法等)并希望写成中文文章
- 用户说"写一篇公众号文章"、"写成 markdown"、"帮我写一篇"
- 用户希望把内容转化为微信公众号 / 知乎 / 掘金 / 小红书可发布的图文
- 用户说"独立成文"、"复制即用"、"不要放在一起"

## 工作流程总览

```
1. 识别素材类型 → 决定使用哪个模式
2. 加载对应模式文件 → 知道这类素材该问什么、怎么找信息
3. 研究素材 → 用工具获取真实信息
4. 应用通用规则 + 模式专用规则 → 写文章
5. 保存为独立 .md 文件
```

## 第一步:识别素材类型(关键)

根据用户提供的素材,**自动判断**属于哪种类型,然后**读取对应的 mode 文件**:

| 素材类型 | 触发信号 | 加载模式 |
| :--- | :--- | :--- |
| **GitHub 开源项目** | github.com 链接 / 项目名 + repo / "开源项目" | `modes/github-project.md` |
| **新闻事件** | 新闻链接 / "XX 发布"/"XX 事件" / 时事话题 | `modes/news-event.md` |
| **推特/X 帖子** | x.com 或 twitter.com 链接 / "这条推文"  | `modes/twitter-post.md` |
| **学术论文** | arxiv.org 链接 / 论文标题 / "这篇 paper" | `modes/research-paper.md` |
| **产品评测** | 产品官网 / "评测一下 XX" / "XX 用起来怎么样" | `modes/product-review.md` |
| **教程指南** | "怎么做 XX" / "教程" / "保姆级" | `modes/tutorial-guide.md` |
| **观点/思考文** | "我觉得 XX" / "聊聊 XX" / "对 XX 的看法" | `modes/opinion-essay.md` |
| **工具/福利推荐** | "免费"/"白嫖"/"领取"/"福利" | `modes/freebie-deal.md` |
| **多素材合写** | 多个不同类型素材一起出现 | 分别识别,各自走对应模式 |
| **不确定** | 无法明确归类 | 询问用户 / 默认 `modes/general.md` |

### 识别策略

1. 看 URL 域名(github.com / arxiv.org / x.com 等)
2. 看用户的关键词("项目"/"新闻"/"论文"/"福利"等)
3. 不确定时,**最多问一个澄清问题**,但要先给出你的猜测让用户确认

## 第二步:读取通用规则 + 模式规则

**永远先读:** `references/core-writing-rules.md`(中文写作通用规范)

**然后按需读:**
- 对应的 `modes/{mode}.md` 文件
- 需要选标题时:`references/title-patterns.md`
- 需要避雷时:`references/avoid-list.md`
- 需要研究指引时:`references/research-playbook.md`
- 不确定结构时:`references/article-structures.md`

## 第三步:研究素材(必须真实,禁止编造)

**核心原则:不基于训练数据猜测,所有事实必须实时验证。**

各模式的 mode 文件会指导你**该用哪些工具**、**该问哪些问题**、**该从哪里找信息**。

通用工具:
- `web_fetch` — 抓取网页内容(GitHub / 新闻 / arXiv / 推特等)
- `web_search` — 搜索补充信息、找中文资料
- `image_search` — 需要插图时(谨慎使用)

## 第四步:写作

### 永远遵守的核心铁律

1. **每个独立素材,生成独立 .md 文件**(N 个 → N 个,绝不合并)
2. **文件名:** `{主题简称}-公众号文章.md`(中英混合,简洁可识别)
3. **保存位置:** `/mnt/user-data/outputs/`(优先) → `/home/claude/`(备选)
4. **长度:** 2500-4500 中文字符为主,极特殊情况不超过 5500 字
5. **中文原生写法**,不是翻译腔
6. **真实信息**,不编造数据
7. **结构化**,但不刻板;每篇都按"开头钩子→主体→收尾"的节奏

### 结构选择

不同模式有不同的推荐结构。读取 `modes/{mode}.md` 时会得到该模式的最佳结构。

**通用骨架(所有文章共有):**
```
标题
> 副标题/精华引述
---
开头钩子(共鸣场景)
主体(分节展开,密度高)
价值/影响/总结
收尾(不鸡汤,有具体反思)
信息表格(便于读者收藏)
互动话题
```

## 第五步:输出

### 单个素材
- 创建 `{主题}-公众号文章.md`
- 调用 `present_files`(如果环境支持)

### 多个素材
- **每个独立一个文件**
- 全部生成完后,一次性 `present_files`
- 用一段简短文字总结(不复述内容)

### 输出后的话术

简短即可,**不要复述文章内容**,例:

> 已生成 X 篇文章:
> - 文件 1:核心亮点(一句话)
> - 文件 2:核心亮点(一句话)
> 都在 outputs 目录,可直接复制粘贴发布。

## 跨工具兼容

此 skill 设计为**模型/工具无关**:

- ✅ Claude Code:放进 `~/.claude/skills/wechat-article-writer/`,自动加载
- ✅ Cursor / Windsurf:放进 `.cursor/rules/` 或作为系统提示词
- ✅ ChatGPT / Gemini / 通义 / DeepSeek:用 `single-file-prompt.md`(合并版)作为 system prompt
- ✅ 普通对话:用户复制粘贴对应 mode + 通用规则即可

## 重要文件索引

### 通用层(每次都要读)
- `references/core-writing-rules.md` — 中文写作规范,基本功
- `references/article-structures.md` — 文章骨架的多种变体

### 工具层(按需读)
- `references/title-patterns.md` — 11 种标题模式
- `references/avoid-list.md` — 写作雷区清单
- `references/research-playbook.md` — 研究取材方法论

### 模式层(按素材类型读对应一个)
- `modes/github-project.md`
- `modes/news-event.md`
- `modes/twitter-post.md`
- `modes/research-paper.md`
- `modes/product-review.md`
- `modes/tutorial-guide.md`
- `modes/opinion-essay.md`
- `modes/freebie-deal.md`
- `modes/general.md` — 兜底通用模式

### 示例
- `examples/example-github.md` — GitHub 项目文章范例
- `examples/example-news.md` — 新闻文章范例
- `examples/example-paper.md` — 论文文章范例

## 一份精华原则,贴在脑门上

1. **真实** > 全面 — 信息必须查证,宁可少写不可编造
2. **共鸣** > 高深 — 让读者觉得"这说的就是我"
3. **密度** > 长度 — 每段都要有新信息,不灌水
4. **结构清晰** > 文采华丽 — 公众号读者扫读,要让骨架明显
5. **独立成文** > 大而全 — 一个素材一篇,不堆砌
6. **中文母语** > 翻译腔 — 像和朋友聊天,不像维基百科
