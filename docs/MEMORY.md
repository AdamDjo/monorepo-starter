# Project Memory

## Quick Summary

- **Project**: <!-- set by "go new-project" -->
- **Repo**: `<owner>/<repo>` <!-- update after setup -->
- **npm scope**: `@starter/*` <!-- update after setup -->
- **Current phase**: Phase 1 — Foundation
- **Branch**: main / develop

---

## Project State

<!-- Updated by "go new-project" and maintained each session -->

### Stack

- Frontend: Next.js 15 (App Router) + TypeScript + Tailwind CSS
- Backend: Express + TypeScript
- Database: Supabase
- AI: <!-- add providers here -->

### GitHub

- Scrum Board PROJECT_ID: `<PROJECT_ID>` <!-- set after creating project board -->
- Labels: created via `.github/setup-github.sh`
- Milestones: Phase 1 / Phase 2 / Phase 3

---

## Timeline

<!-- Key decisions and events -->

- [ ] Project initialized with "go new-project"
- [ ] GitHub labels and milestones configured
- [ ] Renovate installed
- [ ] Phase 1 development started

---

## Key Decisions

<!-- Architecture choices and why -->

---

## User Preferences

- Language: <!-- French / English -->
- Commits: no `Co-Authored-By` Claude
- Format commit: `type(scope): message`
- Sequential work (no parallel agents unless explicitly requested)

---

## Next Steps

1. Type **"go new-project"** to initialize your project (Claude will brainstorm with you)
2. `bash .github/setup-github.sh` — create GitHub labels + milestones
3. Install Renovate: https://github.com/apps/renovate
4. `pnpm dev` — start locally
5. `/feature <name>` — start your first feature

---

## How Claude assists on this project

At the start of every session, Claude reads this file to know the current project state.

**Available commands:**

| Command | Action |
|---|---|
| `go new-project` | Brainstorm + full project initialization |
| `/feature <name>` | Create a GitHub issue + feature branch from develop |
| `/bug <name>` | Create a bug issue + fix branch |
| `/hotfix <name>` | Create an issue + hotfix branch from main |
| `/pr` | Push the branch and open a PR with labels/milestone |
| `/release <version>` | Create the release branch (triggers CI) |
| `/sync` | Sync develop with main after hotfix/release |
| `/docs` | Update MEMORY.md + ARCHITECTURE.md from the current code state |
| `/implement <desc>` | Full feature implementation workflow |
| `/check` | Run lint + type-check across the monorepo |
| `/status` | Show current phase, branch, and next tasks |
