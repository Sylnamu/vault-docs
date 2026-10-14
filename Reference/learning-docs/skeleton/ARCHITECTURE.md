# ARCHITECTURE.md

> 中文导读：给贡献者看的 Explanation。Google Ch.10 要求：目标→策略→多方案权衡→专家评审点。写在写代码前，过评审再开工。

## Goals / Non-goals

- Goals:
- Non-goals:

## Context & Constraints

- Who uses it, scale, compat (e.g. App vs Pages 双轨？next.js 用 `docs/01-app/02-pages` 并列处理迁移期）

## Options Considered

| Option | Pros | Cons |
|---|---|---|
| A | | |
| B | | |

- Decision: (link to `decisions/ADR-0001-*.md`)

## Modules

- `src/...`: responsibility + invariants
- Data flow (one diagram, ascii ok):

```
request -> router -> handler -> store
```

## Cross-cutting

- Security / i18n / storage / privacy / a11y (Google 模板强制项，缺的写 N/A + 理由）
- Errors: each user-facing error gets `errors/<code>.md` equivalent (学 next.js `errors/*.mdx` 按码建档，CLI 直接链过去）

## History

- After landing, revisit: did we meet Goals? Archive as record, don't delete.

## Sources / 引用

- Google 设计文档要求 (SWE Book Ch.10): https://abseil.io/resources/swe-book/html/ch10.html
- 活例 next.js 架构文档: https://github.com/vercel/next.js/tree/canary/docs
