---
project_name: 'Pi-Obsy'
user_name: 'µ'
date: 'Saturday, May 2, 2026'
sections_completed: ['technology_stack', 'critical_rules', 'conventions']
existing_patterns_found: 12
---

# Project Context for AI Agents

_This file contains critical rules and patterns that AI agents must follow when implementing code in this project. Derived from AGENTS.md and project structure._

---

## Technology Stack & Versions

- **Runtime**: Node.js >= 20.0.0
- **Language**: TypeScript ^5.9.2
- **Monorepo**: NPM Workspaces
- **Lint/Format**: Biome 2.3.5
- **Tooling**: Husky, Concurrently, Tsx, Shx
- **Key Modules**:
  - `pi-ai`: Multi-provider LLM API
  - `pi-agent-core`: Tool calling & state management
  - `pi-coding-agent`: CLI Agent
  - `pi-tui`: Differential rendering Terminal UI
  - `pi-web-ui`: Web chat components

---

## Critical Implementation Rules

### 🛠 Development Workflow
- **Validation**: `npm run check` MUST be run after any code change. All errors, warnings, and infos must be fixed.
- **Forbidden Commands**: NEVER run `npm run dev`, `npm run build`, or `npm test` unless explicitly asked.
- **Testing**: Run tests from the specific package root, not the repo root. For `coding-agent`, use `test/suite/harness.ts`.

### 💻 Coding Standards
- **Types**: No `any` types unless absolutely necessary. Check `node_modules` for external types.
- **Imports**: **NEVER use inline or dynamic imports** (e.g., no `await import`). Always use top-level standard imports.
- **ESM**: Use `.js` extensions in imports where required by the ESM setup.
- **Hardcoding**: No hardcoded key checks; all keybindings must be configurable via `DEFAULT_*_KEYBINDINGS`.

### 📝 Style & Communication
- **Tone**: Technical, concise, no fluff, no cheerful filler.
- **Formatting**: Indent with **tabs** (width 3). Max line width 120. Managed by Biome.
- **Visuals**: No emojis in commits, code, or PR comments.

---

## Git & Collaboration Rules

### 🚦 Parallel Agent Safety
- **Staging**: NEVER use `git add .` or `git add -A`. List specific file paths only.
- **Destructive Ops**: NEVER use `git reset --hard`, `git checkout .`, `git clean -fd`, or `git stash`.
- **Commits**: Only commit files you changed in the current session. Include `fixes #<number>` for related issues.
- **Pushing**: Use `git pull --rebase && git push`. Abort rebase if conflicts occur in files you didn't touch.

---

## Project Structure Conventions

- **Packages**: Located in `/packages/*`.
- **Changelogs**: Each package has its own `CHANGELOG.md`. Follow the `[Unreleased]` structure.
- **Models**: Never modify `packages/ai/src/models.generated.ts` directly; update the generation script instead.
