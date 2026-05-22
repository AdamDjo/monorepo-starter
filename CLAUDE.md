# Monorepo Starter — Claude Code Instructions

## IMPORTANT: Project Memory

**Claude: Always read `docs/MEMORY.md` at the start of each session.** It contains persistent project state, user preferences, and implementation notes that carry across conversations.

## ⚠️ IMPORTANT: Git Commit Rules

**Always apply these rules for every commit, no exceptions:**

- **No Claude auto-generated `Co-Authored-By`** — never add `Co-Authored-By: Claude ... <noreply@anthropic.com>`. Co-Authored-By for real collaborators is allowed.
- **Clear and descriptive message** — explain what was done and why, not just a generic list
- **Format**: `type(scope): short summary` + blank line + detailed explanation if needed
- **Types**: `feat`, `fix`, `chore`, `docs`, `refactor`, `test`

## First Session Checklist — "go new-project"

When the user types **"go new-project"**, run this checklist sequentially:

1. **Ask these questions one by one:**
   - "What's the name of your project?"
   - "Give me a short description (1-2 sentences)"
   - "What's the main feature or purpose?"
   - "Frontend stack: Next.js 15 (default) or something else (React+Vite, Remix, etc.)?"
   - "Backend stack: Express (default) or something else (NestJS, FastAPI, Hono, etc.)?"
   - "Database: Supabase (default), Postgres+Prisma, MongoDB, or other?"
   - "Do you want AI integration? If yes, which provider(s)? (OpenAI, Claude, Gemini, Mistral)"

2. **After collecting answers:**
   - Generate `docs/PRODUCT_DESIGN.md` with project vision, features, user stories
   - Generate `docs/ARCHITECTURE.md` with tech choices, data model, API design
   - Update `docs/MEMORY.md` with project name, description, stack, phase
   - Update `CLAUDE.md` (this file): replace `@starter/*` with `@<project-scope>/*`, update project description
   - Update all `package.json` files: replace `@starter/*` with `@<project-scope>/*`

3. **GitHub setup:**
   - Create GitHub milestones: Phase 1 — Foundation, Phase 2 — MVP, Phase 3 — Polish
   - Create Phase 1 issues from PRODUCT_DESIGN.md
   - Remind user to run: `bash .github/setup-github.sh` to create labels

4. **Git setup:**
   - Create `develop` branch from `main`
   - Push `develop` to remote

5. **Confirm with summary:**
   ```
   ✅ Project initialized: <name>
   ✅ docs/PRODUCT_DESIGN.md generated
   ✅ docs/ARCHITECTURE.md generated
   ✅ docs/MEMORY.md updated
   ✅ Milestones created: Phase 1 / 2 / 3
   ✅ Phase 1 issues created
   ✅ develop branch created

   Next: /feature <issue-name> to start your first feature
   ```

## Tech Stack (defaults — configurable via "go new-project")

- **Monorepo**: Turborepo (pnpm workspaces)
- **Frontend**: Next.js 15 (App Router) + TypeScript + Tailwind CSS
- **Backend**: Node.js + Express + TypeScript
- **Database**: Supabase (PostgreSQL + Auth + Storage)
- **AI**: Multi-provider (OpenAI, Claude, Mistral, Gemini) with fallback chain
- **State**: Zustand (client) + React Query (server state)

## npm Scope

Default scope: `@starter/*`

**After running "go new-project"**: Claude renames `@starter/*` → `@<your-scope>/*` automatically in all files.

---

## Dependencies — universal vs stack-specific

### Always present (every project, never remove)

**Root:** Turborepo, pnpm, Husky, commitlint, lint-staged, Knip

**Both apps:**
- `zod` — validation, framework-agnostic
- `@<scope>/eslint-config` + `@<scope>/prettier-config` — linting/formatting
- `typescript`, `eslint`, `prettier`
- `vitest` + `@vitest/coverage-v8` — unit tests
- `dotenv` — env vars (backend)

**packages/shared:** `ApiResponse<T>`, `PaginatedResponse<T>` — always keep, add your types here

### Stack-specific (swapped by "go new-project")

**Frontend framework:**
| Choice | Deps added | Deps removed |
|---|---|---|
| Next.js 15 (default) | `next`, `react`, `react-dom`, `eslint-config-next`, `@next/bundle-analyzer` | — |
| React + Vite | `vite`, `@vitejs/plugin-react` | `next`, `eslint-config-next`, `@next/bundle-analyzer` |
| Remix | `@remix-run/*` | `next`, `zustand`, `@tanstack/react-query` |
| SvelteKit | `@sveltejs/kit`, `svelte` | all React/Next deps |

**React UI libs (kept for any React-based frontend):**
`zustand`, `@tanstack/react-query`, `axios`, `react-hook-form`, `lucide-react`, `framer-motion`

**Backend framework:**
| Choice | Deps added | Deps removed |
|---|---|---|
| Express (default) | `express`, `express-rate-limit`, `cors`, `tsx` | — |
| NestJS | `@nestjs/core`, `@nestjs/common`, `reflect-metadata`, `rxjs` | `express`, `tsx` |
| Hono | `hono` | `express`, `express-rate-limit` |

**Database:**
| Choice | Deps added | Deps removed |
|---|---|---|
| Supabase (default) | `@supabase/supabase-js` | — |
| Postgres + Prisma | `@prisma/client`, `prisma` | `@supabase/supabase-js` |
| MongoDB | `mongoose` | `@supabase/supabase-js` |

**AI providers (added on top, never replacing anything):**
`openai`, `@anthropic-ai/sdk`, `@google/generative-ai`, `@mistralai/mistralai`

## Project Structure

```
<repo>/
├── apps/frontend/          # Next.js 15 app
├── apps/backend/           # Express API
└── packages/shared/        # Shared TypeScript types & constants
```

## Commands

```bash
bash scripts/setup.sh       # First-time setup (install + .env files + husky)
pnpm dev                    # Start all apps in dev mode
pnpm dev --filter frontend  # Start only frontend
pnpm dev --filter backend   # Start only backend
pnpm build                  # Build all
pnpm lint                   # Lint all
pnpm type-check             # TypeScript check all
pnpm test                   # Run all unit tests
```

## Code Conventions

### General

- TypeScript strict mode everywhere
- All types shared between frontend/backend go in `packages/shared`
- Never duplicate types — always import from `@starter/shared`
- Use named exports, not default exports
- Use `async/await`, never raw Promises with `.then()`

### Naming

- Files: `kebab-case.ts` (e.g., `user.service.ts`)
- Types/Interfaces: `PascalCase` (e.g., `UserProfile`, `ApiResponse`)
- Functions/variables: `camelCase`
- Constants: `UPPER_SNAKE_CASE`
- React components: `PascalCase.tsx` (e.g., `UserCard.tsx`)

### Frontend (Next.js)

- App Router — Server Components by default, `'use client'` only when needed
- Components in `src/components/` organized by domain
- Hooks in `src/hooks/`
- All API calls go through proxy route `app/api/[...path]/route.ts`
- Use Zustand for UI state, React Query for server data
- Tailwind CSS for styling, no CSS modules

### Backend (Express)

- Routes in `src/routes/` — thin controllers, delegate to services
- Business logic in `src/services/`
- All responses follow format: `{ success: boolean, data?: T, error?: string }`
- Validate all inputs with zod

## Architecture Rules

- **Backend owns all business logic**
- **Frontend is display-only**: shows data, sends actions
- **Never trust frontend data**: always validate on backend
- **Shared types in `packages/shared`**: never duplicate

## GitHub Workflow

### Branch Strategy

```
main          ← production, protected (PRs only)
develop       ← integration branch, all features merge here
feature/*     ← feature branches
release/*     ← release candidates
hotfix/*      ← urgent production fixes
```

### Branch Naming

```
feature/<issue>-<description>
fix/<issue>-<description>
hotfix/<issue>-<description>
release/<semver>
```

**Absolute rules — no exceptions:**

- Always create the issue before the branch
- Never commit directly to `develop` or `main`
- Use `/feature`, `/bug`, `/hotfix` skills — they create issue + branch automatically

### Workflow Claude → GitHub

- `/feature <name>` → create issue + branch from develop
- `/bug <name>` → create issue + branch from develop
- `/hotfix <name>` → create issue + branch from main
- `/pr` → push branch + open PR with correct labels
- `/release <version>` → create release branch (triggers CI)
- `/sync` → sync develop with main after hotfix/release

### Labels (created by setup-github.sh)

| Label | Usage |
|---|---|
| `type: feature` | New feature |
| `type: bug` | Bug fix |
| `type: chore` | Maintenance |
| `type: docs` | Documentation |
| `type: release` | Release PR |
| `priority: high` | Must fix this sprint |
| `priority: medium` | This week |
| `priority: low` | Backlog |
| `domain: frontend` | `apps/frontend/` |
| `domain: backend` | `apps/backend/` |
| `domain: shared` | `packages/shared/` |
| `domain: devops` | `.github/`, CI |
| `phase: 1` | Foundation |
| `phase: 2` | MVP |
| `phase: 3` | Polish |
| `status: blocked` | Blocked by dependency |

### Milestones

| Milestone | Goal |
|---|---|
| Phase 1 — Foundation | Core infrastructure ready |
| Phase 2 — MVP | Fully working product |
| Phase 3 — Polish | Production-ready |

## Agent Workflow

- **Agent Backend**: works on `apps/backend/` only
- **Agent Frontend**: works on `apps/frontend/` only
- **Agent Shared**: works on `packages/shared/` only
- Always define shared types before backend/frontend implementation
