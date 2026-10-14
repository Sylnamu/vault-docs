# Skills Backlog（暂存，暂不安装）

按 Diataxis 留档，备后续商业化决策用。

## Explanation：为什么留这三个

关注点是约束驱动的判断：付费边界、许可证风险、AI谁扛成本、零成本验证。
- 决策归 `devtools-business-model`
- 定价归 `pricing-strategist`
- 动手验证归 `micro-saas-launcher`

商标方向没找到 installs 过百的靠谱 skill，已剔除。

## Reference：资源清单

### 1. samber/developer-relations-skills@devtools-business-model

作用：定什么免费、什么收钱，open core 还是卖云。
installs：4.5K，已过 Agent Trust Hub / Socket / Snyk。

```bash
npx skills add samber/developer-relations-skills@devtools-business-model
```

https://skills.sh/samber/developer-relations-skills/devtools-business-model

### 2. ncklrs/startup-os-skills@pricing-strategist

作用：订阅和 AI 额度定价。
installs：206。

```bash
npx skills add ncklrs/startup-os-skills@pricing-strategist
```

https://skills.sh/ncklrs/startup-os-skills/pricing-strategist

### 3. davila7/claude-code-templates@micro-saas-launcher

作用：单人零成本发 MVP。
installs：400。

```bash
npx skills add davila7/claude-code-templates@micro-saas-launcher
```

https://skills.sh/davila7/claude-code-templates/micro-saas-launcher

## How-to：以后要用时怎么做

1. 先装第 1 个跑付费边界，输出什么永远免费。
2. 有免费边界后再用第 2 个定额度包和超量策略。
3. 要动手了再装第 3 个发最小可用版。
4. 验质量只看三项：installs 是否过百、来源是否官方或高星、是否有安全审计。13 installs 的 `opensource-guide-coach` 已按此规则丢弃。

## Tutorial：首次走通路径

等笔记项目要定商业模式时，按顺序问：
先问“用户在哪一刻非付不可”，再问“AI额度怎么计量”，最后问“最小可收费版本是什么”。三个 skill 各答一问。
