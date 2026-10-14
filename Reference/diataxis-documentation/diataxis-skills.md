# Diataxis Skills（暂存，暂不安装）

按 Diataxis 留档，备后续文档/笔记项目用。官网基座：https://www.diataxis.fr

## Explanation：为什么留这两个

都是以 Diataxis 四象限（Tutorial / How-to / Reference / Explanation）为基座，但哲学不同，互补：

- `sammcj` 是创作派：关心文档“用起来什么感觉”，讲 flow、语气、责任归属，让结构从内容里长出来。适合写新文档。
- `pproenca` 是诊断派：核心是 type-mixing，一段内容服务多个需求就是病，拆开就好。带决策树+脚本+审计模板。适合修老文档堆。

同时装会双触发（触发词高度重叠：`write docs / README混乱 / tutorial vs how-to`），文件层面不覆盖（目录名不同），但只留一个即可。

## Reference：资源清单

### 1. sammcj/agentic-coding@writing-documentation-with-diataxis

作用：写新文档/改单篇，认人 → 罗盘定位 → 按文体写 → 查边界拆分。
哲学：Diataxis 是 approach 不是 template；flow 最重要；structure follows content。
installs：611，已过 Agent Trust Hub / Socket / Snyk。
来源星数：sammcj/agentic-coding 162 stars。
注意：上游当前在 `Skills_disabled/diataxis-documentation` 下，skills.sh 快照仍可装，安装后核对 `name: writing-documentation-with-diataxis` 是否存在。

```bash
npx skills add sammcj/agentic-coding@writing-documentation-with-diataxis
```

https://skills.sh/sammcj/agentic-coding/writing-documentation-with-diataxis

### 2. pproenca/dot-skills@diataxis

作用：修混乱文档集，症状表 → 四棵决策树 → 小步迭代 → 留审计档。
哲学：大多数文档问题就是 type-mixing；descriptive not prescriptive；配 `scan-docs.sh`、`quality.md`、`report.md`、`config.json(docs_root)`。
installs：125，已过 Agent Trust Hub / Socket / Snyk。
来源星数：pproenca/dot-skills 214 stars。
上游路径：`skills/.experimental/diataxis`。

```bash
npx skills add pproenca/dot-skills@diataxis
```

https://skills.sh/pproenca/dot-skills/diataxis

### 已剔除

- `rlespinasse/agent-skills@diataxis`：184 installs 但仓库仅 12 stars，按过百星规则丢弃。
- 个人笔记/PKM 方向（`pkm-documentation` 32 installs、`obsidian-organizer` 6 installs）无 Diataxis 基座且量级太低，已剔除。

## How-to：以后要用时怎么做

1. 写新文档只装第 1 个，输出时要求注明用了哪种文体、为什么。
2. 接手老文档堆只装第 2 个，先跑 `scan-docs.sh` 再按症状表进树，不要全量重构。
3. 验质量只看三项：installs 是否过百、来源是否高星、是否有安全审计。
4. 两个不同时装，避免双触发。

## Tutorial：首次走通路径

等笔记/文档项目启动时，按顺序问：
先问“这篇服务谁、在学还是在干”，再问“罗盘落到哪个象限”，最后问“有没有混进别象限的内容要拆出去”。第 1 个 skill 答写法，第 2 个 skill 答修法。
