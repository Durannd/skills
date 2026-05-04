# Bootstrap Template

Copy this file into your project as `GEMINI.md` (for Gemini) or `CLAUDE.md` (for Claude) to wire the full skills framework into your AI assistant.

Replace `<PATH_TO_SKILLS>` with the relative or absolute path where this repository is installed (e.g. `.agent/skills` or `~/skills`).

---

```markdown
# AI Assistant Configuration

## Skills Location
skills-root: <PATH_TO_SKILLS>

---

## TIER 0 — Always Active (loaded on every request)

skills:
  - <PATH_TO_SKILLS>/skills/intelligent-routing/SKILL.md   # auto-routes requests to the right agent
  - <PATH_TO_SKILLS>/skills/clean-code/SKILL.md            # baseline coding standards
  - <PATH_TO_SKILLS>/skills/behavioral-modes/SKILL.md      # adapt AI behavior per task type

## TIER 1 — Routing Rules

The `intelligent-routing` skill is already active. It will:
1. Analyze every user request for domain keywords and complexity.
2. Silently select and apply the most relevant specialist agent.
3. Announce the selected agent inline: `🤖 Applying knowledge of @<agent>...`

You can override auto-routing at any time:
  - Explicit agent: `@backend-specialist add rate limiting`
  - Explicit skill:  `@svelte-expert refactor this component`

## TIER 2 — Available Agents

Agents are loaded on demand by the routing layer. Do not pre-load all agents.

| Agent | Trigger keywords |
|-------|-----------------|
| orchestrator | complex, multi-domain, full feature, architectural change |
| backend-specialist | api, server, node, python, fastapi, endpoint, auth |
| frontend-specialist | svelte, react, component, css, tailwind, ui, ux |
| database-architect | database, schema, sql, migration, query, prisma |
| security-auditor | security, vulnerability, owasp, xss, injection, pentest |
| test-engineer | test, spec, coverage, jest, playwright, e2e |
| devops-engineer | deploy, production, ci/cd, docker, rollback |
| debugger | bug, error, crash, not working, broken |
| performance-optimizer | slow, optimize, performance, bundle, memory |
| explorer-agent | audit, analyze repo, investigate, reverse engineer |
| product-owner | requirements, user story, backlog, MVP, PRD |
| project-planner | new project, plan feature, dependency graph |
| documentation-writer | readme, api docs, changelog, document |
| code-archaeologist | legacy, spaghetti, undocumented, refactor plan |

## TIER 3 — Workflows (Slash Commands)

Available commands (defined in `<PATH_TO_SKILLS>/workflows/`):

| Command | Purpose |
|---------|---------|
| /create | Scaffold a new full-stack application |
| /enhance | Add features to an existing project |
| /plan | Generate a project plan (no code) |
| /brainstorm | Structured idea exploration |
| /debug | Systematic bug investigation |
| /test | Generate and run tests |
| /deploy | Production deployment wizard |
| /orchestrate | Explicit multi-agent coordination |
| /preview | Manage local dev server |
| /status | Show project and agent status |
| /ui-ux-pro-max | AI-powered design system |

## TIER 4 — Project Context (fill in for your project)

project-name: <YOUR_PROJECT_NAME>
tech-stack: <e.g. SvelteKit, Node.js, PostgreSQL>
primary-language: <e.g. TypeScript>
test-framework: <e.g. Vitest, Playwright>
deploy-target: <e.g. Vercel, Railway, AWS>

## Notes

- Skills are discovered automatically via `SKILLS_INDEX.json` at the skills root.
- To find additional skills: `npx skills find <query>` or visit https://skills.sh/
- To create a new skill: invoke the `write-a-skill` skill or run `npx skills init <name>`
- Caveman mode (compact responses): say "caveman mode" or "/caveman"
```
