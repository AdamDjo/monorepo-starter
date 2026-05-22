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

1. Tape **"go new-project"** pour initialiser le projet (Claude va brainstormer avec toi)
2. `bash .github/setup-github.sh` — créer labels + milestones GitHub
3. Installer Renovate : https://github.com/apps/renovate
4. `pnpm dev` — démarrer en local
5. `/feature <nom>` — démarrer ta première feature

---

## Comment Claude t'assiste sur ce projet

Au démarrage de chaque session, Claude lit ce fichier pour connaître l'état du projet.

**Commandes disponibles :**

| Commande | Action |
|---|---|
| `go new-project` | Brainstorming + initialisation complète du projet |
| `/feature <nom>` | Crée une issue GitHub + branche feature depuis develop |
| `/bug <nom>` | Crée une issue bug + branche fix |
| `/hotfix <nom>` | Crée une issue + branche hotfix depuis main |
| `/pr` | Pousse la branche et ouvre une PR avec labels/milestone |
| `/release <version>` | Crée la branche release (déclenche CI) |
| `/sync` | Sync develop avec main après hotfix/release |
| `/docs` | Met à jour MEMORY.md + ARCHITECTURE.md depuis l'état du code |
| `/implement <desc>` | Workflow complet d'implémentation d'une feature |
| `/check` | Lance lint + type-check sur tout le monorepo |
| `/status` | Affiche phase courante, branche, prochaines tâches |
