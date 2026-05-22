<div align="center">

# claude-stack

**The monorepo template that sets itself up.**

Type `go new-project` in Claude Code. Claude asks what you're building, proposes features, and configures everything — docs, GitHub issues, branches, dependencies — automatically.

[![Use this template](https://img.shields.io/badge/Use%20this%20template-2ea44f?style=for-the-badge&logo=github&logoColor=white)](https://github.com/AdamDjo/claude-stack/generate)
&nbsp;
[![CI](https://github.com/AdamDjo/claude-stack/actions/workflows/ci.yml/badge.svg)](https://github.com/AdamDjo/claude-stack/actions/workflows/ci.yml)
&nbsp;
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

</div>

---

## Why this template?

Most monorepo starters give you a folder structure and leave you to figure out the rest. This one goes further.

**Built-in AI workflow** — Claude Code agents and skills are pre-configured so your entire dev cycle (issues → branch → code → PR → release) runs from natural language commands, not manual steps.

**`go new-project` auto-configures your project** — Claude brainstorms with you, proposes features, then generates your product docs, renames the npm scope, swaps stack-specific deps, and creates your GitHub milestones and Phase 1 issues. In one conversation.

**Production tooling from day one** — ESLint, Prettier, Husky, commitlint, Vitest, Playwright, CodeQL, Renovate, Docker, Turborepo caching — all wired up and working before you write a single line of business logic.

---

## See it in action

```
$ claude   # open Claude Code in your project

> go new-project

  Tell me about your project — what's the idea, who is it for?

> I want to build a SaaS for freelancers to send invoices and get paid online

  Got it — an invoicing platform for freelancers. Here's what I think the
  core features should be:

  1. Invoice builder — create, preview, and send PDF invoices
  2. Payment links — Stripe integration, one-click payment for clients
  3. Dashboard — revenue overview, unpaid invoices, client history
  4. Client management — contact book linked to invoice history
  5. Recurring invoices — auto-send monthly invoices for retainer clients

  A couple of risks to keep in mind:
  - Stripe webhooks need careful handling (idempotency, retry logic)
  - PDF generation can be slow — consider async generation + S3 storage

  Does this match your vision? Anything to add or remove?

> Perfect, let's keep it. I'll use the default stack (Next.js + Express + Supabase)
  GitHub: johndoe/invoicer  scope: @invoicer

  ✅ docs/PRODUCT_DESIGN.md generated   — vision, features, user stories
  ✅ docs/ARCHITECTURE.md generated     — data model, API routes, stack decisions
  ✅ docs/MEMORY.md updated             — project state (read every session)
  ✅ @starter/* renamed to @invoicer/*  — all package.json, tsconfig, configs
  ✅ Milestones created                 — Phase 1 / Phase 2 / Phase 3
  ✅ 6 Phase 1 issues created           — ready in your GitHub backlog
  ✅ develop branch created and pushed

  Start coding: /feature invoice-builder

> /feature invoice-builder

  ✅ Issue #1 created — "feat: invoice builder"
  ✅ Branch feature/1-invoice-builder created from develop

  Commit: git commit -m "feat(invoices): <description>"
  When ready: /pr
```

---

## What you get

### Pre-configured tooling

| Category  | Tool                                 | Details                                            |
| --------- | ------------------------------------ | -------------------------------------------------- |
| Monorepo  | Turborepo + pnpm workspaces          | Parallel builds, shared cache                      |
| Frontend  | Next.js 15, React 19, Tailwind CSS 4 | App Router, SSR, TypeScript strict                 |
| Backend   | Express + Zod                        | Typed routes, input validation                     |
| Database  | Supabase                             | PostgreSQL + Auth + Storage                        |
| Linting   | ESLint v9 flat config + Prettier     | Shared configs across all workspaces               |
| Testing   | Vitest + Playwright                  | Unit tests + E2E with auto-started dev server      |
| Git hooks | Husky + commitlint + lint-staged     | Conventional commits enforced                      |
| CI        | GitHub Actions                       | Lint → type-check → test → build → E2E on every PR |
| Releases  | Automated via `release.yml`          | Tag + GitHub Release from `release/*` branches     |
| Security  | CodeQL                               | Weekly static analysis                             |
| Deps      | Renovate                             | Auto-merges patch/minor updates                    |
| Docker    | Multi-stage builds + dev compose     | Hot-reload in dev, optimized images for prod       |

### Claude Code agents

| Agent           | Role                                                                       |
| --------------- | -------------------------------------------------------------------------- |
| `project-setup` | Runs `go new-project` — brainstorms, generates docs, configures everything |
| `frontend-dev`  | Works on `apps/frontend/` — Next.js, components, hooks                     |
| `backend-dev`   | Works on `apps/backend/` — routes, services, middleware                    |
| `code-reviewer` | Reviews code quality, security, and best practices                         |

### Daily workflow commands

Type these inside Claude Code — no manual git, no copy-pasting issue numbers:

| Command           | What it does                                               |
| ----------------- | ---------------------------------------------------------- |
| `go new-project`  | Full guided setup — brainstorming to first GitHub issue    |
| `/feature <name>` | Create issue + `feature/<n>-<name>` branch from develop    |
| `/bug <name>`     | Create issue + `fix/<n>-<name>` branch                     |
| `/hotfix <name>`  | Urgent fix — branch from main, PR to main                  |
| `/pr`             | Push branch + open PR with correct labels and milestone    |
| `/release 1.0.0`  | Cut release branch → CI → tag → GitHub Release             |
| `/sync`           | Sync develop with main after hotfix or release             |
| `/docs`           | Update MEMORY.md + ARCHITECTURE.md from current code state |
| `/check`          | Run lint + type-check across the whole monorepo            |
| `/status`         | Current phase, open issues, next tasks                     |

---

## Project structure

```
your-project/
├── apps/
│   ├── frontend/          # Next.js 15 — App Router, Tailwind CSS 4, React Query, Zustand
│   └── backend/           # Express — Zod validation, Supabase, rate limiting
├── packages/
│   ├── shared/            # TypeScript types shared between frontend and backend
│   ├── eslint-config/     # Shared ESLint flat configs (base, next, backend)
│   └── prettier-config/   # Shared Prettier config
├── docs/
│   ├── MEMORY.md          # Project state — Claude reads this at the start of every session
│   ├── PRODUCT_DESIGN.md  # Generated by go new-project
│   └── ARCHITECTURE.md    # Generated by go new-project
├── .github/
│   ├── workflows/         # CI, release, CodeQL, Docker publish
│   ├── ISSUE_TEMPLATE/    # Bug, feature, chore templates
│   └── setup-github.sh    # Creates labels + milestones on your repo
├── .claude/
│   ├── agents/            # Claude Code agents (project-setup, frontend, backend, reviewer)
│   └── skills/            # Slash commands (/feature, /bug, /pr, /release, /sync...)
└── scripts/
    └── setup.sh           # First-time setup (install + .env files + git hooks)
```

---

## Get started

### Prerequisites

- [Node 20+](https://nodejs.org)
- [pnpm 9+](https://pnpm.io/installation)
- [Claude Code](https://claude.ai/code)
- [GitHub CLI](https://cli.github.com) — for `/feature`, `/pr`, and all GitHub skills

### 1. Create your repo from this template

Click **"Use this template"** at the top of this page, or:

```bash
git clone https://github.com/AdamDjo/claude-stack.git <your-project>
cd <your-project>
```

### 2. Install dependencies and configure git hooks

```bash
bash scripts/setup.sh
```

### 3. Set up GitHub labels and milestones

```bash
bash .github/setup-github.sh
# Interactive — asks for your 3 phase names, then creates all labels and milestones
```

### 4. Open Claude Code and initialize your project

```bash
claude
```

Then type:

```
go new-project
```

That's it. Claude takes it from there.

---

## Configurable defaults

`go new-project` swaps everything based on your answers. Default stack is Next.js 15 + Express + Supabase — change any layer:

| Layer    | Default    | Alternatives                       |
| -------- | ---------- | ---------------------------------- |
| Frontend | Next.js 15 | React + Vite, Remix, SvelteKit     |
| Backend  | Express    | NestJS, Hono, FastAPI              |
| Database | Supabase   | Postgres + Prisma, MongoDB, SQLite |
| AI       | none       | OpenAI, Claude, Gemini, Mistral    |

The npm scope `@starter/*` is renamed to `@<your-scope>/*` in all files automatically.

---

## MCP setup (recommended)

MCP gives Claude direct access to your GitHub repo and Supabase project — required for `/feature`, `/pr`, `/create-issues` and other GitHub skills.

```bash
cp .mcp.json.example .mcp.json
# Fill in GITHUB_TOKEN and SUPABASE credentials
```

---

## License

MIT
