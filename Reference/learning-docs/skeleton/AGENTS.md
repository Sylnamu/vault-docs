# AGENTS.md — README for agents (and new humans)

> 中文导读：这是给 Agent/新人看的执行手册，不是给用户看的。保持可执行、无废话。规范见 https://agents.md/ ：monorepo 可嵌套，就近优先。
> 对照 next.js 根 AGENTS.md：monorepo地图 + 构建矩阵 + 测法 + PR规则 + secrets红线。

## Map

- Stack: TypeScript + Node.js + pnpm (change to yours)
- Packages: `packages/*` (if monorepo, each dir may have own AGENTS.md/README, read nearest first)
- Docs: `docs/` for users, `decisions/` for ADRs, `product/` for PRD

## Build / Dev

```bash
pnpm install
pnpm build
pnpm dev
```

## Test / Lint (run before PR)

```bash
pnpm test
pnpm lint
pnpm typecheck
```

- next.js 教训：有 4 种测法（test-dev-turbo 等），你至少区分 `unit` vs `e2e`，PR 里写清跑了哪种。

## PR Rules

- Fork-PR for externals, branch-PR for maintainers.
- Trivial PRs (typo/format only) may be closed — docs exception, same as next.js `contributing.md`.
- Conventional Commits: `feat:`, `fix:`, `BREAKING CHANGE:` (drives SemVer + Changelog).

## Guardrails

- Never commit secrets / `.env`. Minimal `permissions: {}` in workflows (see `.github/AGENTS.md` idea).
- Pin GitHub Actions to commit SHA, not `@v4`.
- Read `ARCHITECTURE.md` + nearest `README` before editing a package.

## Sources / 引用

- AGENTS.md 开放标准: https://agents.md/
- OpenAI 实现指南: https://developers.openai.com/codex/guides/agents-md/
- 活例 next.js 根总纲: https://github.com/vercel/next.js/blob/canary/AGENTS.md
