# CONTRIBUTING.md (thin index — details live in subdirs)

> 中文导读：学 next.js `contributing.md` 做薄，只做索引。细节分流，避免 2000 行大文件。

## I want to...

- Run locally → `docs/tutorial-getting-started.md`
- Add a feature → `decisions/` 先写 ADR，过评审再写码
- Add docs → `docs/` + Diátaxis 对号入座（Tutorial/How-to/Reference/Explanation）
- Add an error link → 新增用户报错必须配 `docs/how-to-*` 或 error 页（学 `contributing/core/adding-error-links`）
- Release → `CHANGELOG.md` + GitHub Releases（Conventional Commits 自动生成）

## Workflow

1. Fork (external) or branch (maintainer).
2. `pnpm install && pnpm test && pnpm lint`
3. Conventional Commits. PR description: What/Why/How tested (see `.github/pull_request_template.md`).
4. Trivial typo/format PRs may be closed (docs exception).

## Governance

- Triage / lint / release channels: (L3 再拆 `contributing/repository/`，L2 先写在这里 10 行）
- Code of Conduct: `CODE_OF_CONDUCT.md`

## Sources / 引用

- 活例 next.js 薄索引模式: https://github.com/vercel/next.js/blob/canary/contributing.md
- 同仓 `.github` 治理实例: https://github.com/vercel/next.js/tree/canary/.github
