# 全场景中文公众号写作助手 (Skill)

把任何素材 → 中文公众号 markdown 文章。

## 是什么

一个**模型无关**的 AI Skill,封装了一套生成高质量中文公众号文章的方法论。

支持 **8 种素材类型**,每种类型都有专属的研究流程、文章结构、写作要点。

## 支持的素材类型

| 素材类型 | 触发关键词 | 推荐结构 |
| :--- | :--- | :--- |
| **GitHub 开源项目** | github.com 链接 | A 介绍型 |
| **新闻事件** | 新闻链接 / 事件描述 | B 事件型 |
| **推特/X 帖子** | x.com / twitter.com | F 推特展开型 |
| **学术论文** | arxiv.org / DOI / paper | D 解读型 |
| **产品评测** | "评测一下"/产品官网 | A 介绍型 |
| **教程指南** | "怎么做"/"教程"/"how-to" | E 教程型 |
| **观点思考文** | "聊聊"/"对 XX 看法" | C 观点型 |
| **福利羊毛** | "免费"/"白嫖"/"领取" | G 福利型 |
| **通用兜底** | 不属于以上任何 | A-I 灵活选择 |

## 核心特性

- 🎯 **8 种专用模式** + **9 种文章结构** + **11 种标题模式**
- 🔍 **真实研究** — 用 web_fetch / web_search 获取素材,不编造
- 🇨🇳 **中文原生写作** — 不是翻译腔,像母语者
- 📐 **完整模板** — 每篇都有共鸣开头、密度主体、有力收尾、信息表格
- ⚠️ **18 条雷区清单** — 系统避开常见错误
- 📂 **每素材独立成文** — N 个素材 → N 个 .md 文件
- 🛠️ **跨工具兼容** — Claude Code / Cursor / ChatGPT / Gemini 等都能用

## 文件结构

```
wechat-article-writer/
├── SKILL.md                          # 主入口 / 路由器
├── README.md                         # 本文件
├── references/                       # 通用层(必读)
│   ├── core-writing-rules.md         # 中文写作规范
│   ├── article-structures.md         # 9 种文章结构
│   ├── title-patterns.md             # 11 种标题模式
│   ├── avoid-list.md                 # 18 条雷区
│   └── research-playbook.md          # 研究方法论
├── modes/                            # 模式层(按需读)
│   ├── github-project.md             # GitHub 项目
│   ├── news-event.md                 # 新闻事件
│   ├── twitter-post.md               # 推特/X 帖子
│   ├── research-paper.md             # 学术论文
│   ├── product-review.md             # 产品评测
│   ├── tutorial-guide.md             # 教程指南
│   ├── opinion-essay.md              # 观点文
│   ├── freebie-deal.md               # 福利羊毛
│   └── general.md                    # 通用兜底
└── examples/                         # 示例输出
    ├── example-github.md             # GitHub 项目示例
    └── example-news.md               # 福利文章示例
```

## 跨工具使用

### 方式一:Claude Code(原生)

放进:
```
~/.claude/skills/wechat-article-writer/
```
或项目级:
```
你的项目/.claude/skills/wechat-article-writer/
```

Claude Code 会自动加载,你说"帮我写一篇公众号文章"时自动触发。

### 方式二:Cursor / Windsurf

放进:
```
你的项目/.cursor/rules/wechat-article-writer/
```

或者把 `SKILL.md` 内容作为 Cursor Rules 配置。

### 方式三:OpenCode / Codex CLI

放进:
```
.opencode/agents/wechat-article-writer/
```

### 方式四:ChatGPT / Gemini / 通义 / DeepSeek 等

把 `single-file-prompt.md`(合并版)的全部内容作为系统提示词喂给模型,然后正常对话:

```
帮我把这个 GitHub 项目写成公众号文章:
https://github.com/owner/repo
```

或:

```
基于这条新闻写一篇公众号:
[新闻链接或描述]
```

### 方式五:普通对话

复制对应 mode + 通用规则到对话开头:

```
请按以下规则,把我接下来给你的素材转换为中文公众号文章:

[贴 SKILL.md]
[贴 references/core-writing-rules.md]
[贴 references/title-patterns.md]
[贴 modes/github-project.md(或对应模式)]

我的素材:
https://github.com/owner/repo
```

## 工作流程

```
1. 用户提供素材(URL / 描述 / 截图)
   ↓
2. AI 识别素材类型,加载对应 mode
   ↓
3. AI 用 web_fetch / web_search 真实研究
   ↓
4. AI 应用通用规则 + 模式专用规则写文章
   ↓
5. 保存为独立 .md 文件,present_files 展示
```

## 输出文件

- 文件名:`{主题简称}-公众号文章.md`
- 保存位置:`/mnt/user-data/outputs/`(优先) 或 当前工作目录
- 多素材时:**每个独立文件**,绝不合并

## 长度规范

| 内容类型 | 推荐长度 |
| :--- | :--- |
| GitHub 项目 | 3000-4500 字 |
| 新闻事件 | 2500-4000 字 |
| 推特展开 | 2000-3500 字 |
| 论文解读 | 3500-5000 字 |
| 产品评测 | 3000-4500 字 |
| 教程指南 | 3000-5000 字 |
| 观点思考 | 2500-4000 字 |
| 福利羊毛 | 2500-4000 字 |

**极限不超过 5500 字**,超长就做减法。

## 常见使用示例

### 示例 1:写 GitHub 项目

**输入:**
```
https://github.com/cline/cline
```

**AI 行动:**
1. 识别为 GitHub 项目
2. 读取 `modes/github-project.md`
3. `web_fetch` GitHub 页面
4. (如需要)`web_search` 中文评测
5. 用结构 A 写文章
6. 输出 `Cline-公众号文章.md`

### 示例 2:写新闻事件

**输入:**
```
英伟达推出免费 1 年 API Key 福利,帮我写一篇文章
```

**AI 行动:**
1. 识别为福利型新闻(混合类型)
2. 读取 `modes/freebie-deal.md`
3. `web_fetch` 英伟达官方
4. `web_search` 申请教程
5. 用结构 G 写文章
6. 输出 `英伟达免费API-领取攻略-公众号文章.md`

### 示例 3:写推特帖子

**输入:**
```
帮我把 Karpathy 这条吐槽 AI 编码的推文写成公众号
https://x.com/karpathy/status/...
```

**AI 行动:**
1. 识别为推特帖子
2. 读取 `modes/twitter-post.md`
3. `web_fetch` 推文(可能失败,改用 search)
4. 核实 Karpathy 身份
5. 找帖子上下文和反应
6. 用结构 F 写文章
7. 输出 `Karpathy-AI编码吐槽-公众号文章.md`

### 示例 4:写论文

**输入:**
```
arxiv.org/abs/2401.12345 这篇论文写成公众号解读
```

**AI 行动:**
1. 识别为学术论文
2. 读取 `modes/research-paper.md`
3. `web_fetch` arXiv 页面
4. 必要时 fetch PDF
5. 找作者背景、同行解读
6. 用结构 D 写文章
7. 输出 `论文主题-论文解读-公众号文章.md`

### 示例 5:批量处理

**输入:**
```
帮我把这些都写成公众号文章,每个独立成文,不要放在一起:
https://github.com/owner/repo1
https://x.com/user/status/123
arxiv.org/abs/2401.xxxxx
```

**AI 行动:**
1. 解析 3 个不同类型的素材
2. **每个素材独立处理**(不合并)
3. 分别加载 github-project / twitter-post / research-paper
4. 各自研究、写作
5. 输出 3 个独立 .md 文件
6. 一次性 present_files 展示

## 高质量文章的标志

每篇交付前,经过 **5 维度自检**:

### 真实性
- [ ] 数据都查证过
- [ ] 时效性确认
- [ ] 没有未核实的指控

### 表达
- [ ] 没翻译腔
- [ ] 没用红词("震惊/逆天/碾压")
- [ ] 中英文之间有空格
- [ ] 中文标点

### 内容
- [ ] 没有正确的废话
- [ ] 每段都有新信息
- [ ] 收尾不鸡汤

### 输出
- [ ] 每素材独立文件
- [ ] 长度在范围内
- [ ] 文件名格式正确

### 安全
- [ ] 不涉政治敏感
- [ ] 不涉个人攻击
- [ ] 不涉违规内容

## 常见问题

### Q1:能否多素材合并写成一篇?

**不能**。`SKILL.md` 中的核心铁律就是"N 个素材 → N 个独立文件"。

如果用户明确要求"合集",可以协商:
- "建议每个独立成文,这样发布更灵活"
- 如果用户坚持,可以做"合集索引"(一篇文章导引+多个独立文件链接)

### Q2:能否用于英文文章?

这个 skill 专为中文设计。语气、节奏、标点规范都是中文特定的。

英文文章建议另起一套规范。

### Q3:素材太冷门搜不到怎么办?

按 `references/research-playbook.md` 的指引:
1. 换关键词、换语言、加修饰
2. 找上下文(机构/作者其他动态)
3. 实在不行,**坦诚告诉用户素材信息有限**,不编造

### Q4:能否生成图片?

skill 输出**纯 markdown 文件**,不包含图片生成。

如果文章需要插图,可以在文中标注"[此处建议截图:...]",让用户后续手动加图。

### Q5:不同模式可以混用吗?

可以,而且经常需要。比如:
- "腾讯开源新福利 API" → 既是新闻 + 福利 + GitHub 项目
- 这种情况主导模式可能是 freebie-deal,但要借鉴 github-project 的结构介绍项目

## 版本历史

- **v1.0**(初版): 单一模式 - GitHub 项目
- **v2.0**(本版): 全场景模式系统 - 8 种素材类型支持

## License

MIT — 自由使用、修改、分发。

## 反馈与改进

这个 skill 设计为"**你自己的**"——所有规则都可以根据你的写作偏好调整:

- 觉得某个模式不够好用 → 改 `modes/` 下对应文件
- 觉得标题模式不够 → 加到 `references/title-patterns.md`
- 写多了发现新的雷区 → 加到 `references/avoid-list.md`

skill 是活的工具,会随着你的使用越来越合身。
