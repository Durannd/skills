# Skills Repository

A modular AI agent framework composed of **skills**, **agents**, **workflows**, and **scripts**. Each piece plays a specific role in turning an LLM into a specialized, domain-aware assistant.

---

## Table of Contents

- [How It All Fits Together](#how-it-all-fits-together)
- [Skills](#skills)
  - [Core / Meta](#core--meta)
  - [Architecture & Planning](#architecture--planning)
  - [Frontend](#frontend)
  - [Backend](#backend)
  - [Database](#database)
  - [Testing & Quality](#testing--quality)
  - [DevOps & Security](#devops--security)
  - [Specialized Tools](#specialized-tools)
- [Agents](#agents)
- [Workflows (Slash Commands)](#workflows-slash-commands)
- [Scripts](#scripts)
- [Usage Tips](#usage-tips)

---

## How It All Fits Together

```
User Request
     │
     ▼
┌─────────────────────────────────────────┐
│           intelligent-routing           │  ← Skill that auto-selects an agent
│  Analyzes keywords → picks specialist   │
└────────────────┬────────────────────────┘
                 │
     ┌───────────▼───────────┐
     │        Agents          │  ← Specialist personas (e.g. backend-specialist)
     │  Each agent loads its  │
     │  own set of skills     │
     └───────────┬───────────┘
                 │
     ┌───────────▼───────────┐
     │        Skills          │  ← Modular knowledge packages
     │  Domain-specific rules │
     │  and best practices    │
     └───────────────────────┘

Workflows = Slash commands that trigger agents + skills in defined sequences.
Scripts   = Python utilities for session state, previews, and verification.
```

| Component | Purpose | Lives in |
|-----------|---------|---------|
| **Skill** | Modular knowledge package loaded by an agent or workflow | `skills/` |
| **Agent** | Specialist persona with a curated skill set | `agents/` |
| **Workflow** | Slash command that wires agents + skills into a flow | `workflows/` |
| **Script** | Python utility for automation and state management | `scripts/` |

---

## Skills

Skills are the building blocks. Each skill lives in its own directory with a `SKILL.md` that contains frontmatter (`name`, `description`, `allowed-tools`) and structured knowledge the LLM loads as context.

### Core / Meta

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [`clean-code`](skills/clean-code/SKILL.md) | Pragmatic coding standards: concise, direct, no over-engineering | Always loaded as a baseline by most agents |
| [`behavioral-modes`](skills/behavioral-modes/SKILL.md) | Defines operational modes: brainstorm, implement, debug, review, teach, ship, orchestrate | Switch the AI's "gear" for a task type |
| [`intelligent-routing`](skills/intelligent-routing/SKILL.md) | Automatic agent selection via keyword/domain detection | Load once in the system prompt to enable zero-command routing |
| [`find-skills`](skills/find-skills/SKILL.md) | Discover and install skills from the open ecosystem (`npx skills`) | When a user asks "is there a skill for X?" |
| [`write-a-skill`](skills/write-a-skill/SKILL.md) | Guide for creating new skills with proper structure and frontmatter | When building a new skill package |
| [`parallel-agents`](skills/parallel-agents/SKILL.md) | Multi-agent orchestration patterns for parallel execution | Complex tasks requiring multiple domain experts simultaneously |
| [`brainstorming`](skills/brainstorming/SKILL.md) | Socratic questioning protocol for clarifying requirements | Before implementing anything complex or ambiguous |
| [`plan-writing`](skills/plan-writing/SKILL.md) | Structured task planning with dependencies and verification criteria | Any multi-step implementation work |
| [`grill-me`](skills/grill-me/SKILL.md) | Relentless interview mode that walks every branch of a decision tree | Stress-testing a design or plan before committing |
| [`caveman`](skills/caveman/SKILL.md) | Ultra-compressed communication mode (~75% token reduction) | When the user wants minimal, dense responses |

### Architecture & Planning

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [`architecture`](skills/architecture/SKILL.md) | ADR-driven architectural decision framework with trade-off analysis | Making system design decisions |
| [`improve-codebase-architecture`](skills/improve-codebase-architecture/SKILL.md) | Finds refactoring opportunities, deepens domain language, improves testability | Architecture audits and refactoring planning |
| [`app-builder`](skills/app-builder/SKILL.md) | Full-stack app creation orchestrator: detects project type, selects tech stack, scaffolds | Starting a new application from scratch |

### Frontend

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [`svelte-expert`](skills/svelte-expert/SKILL.md) | Svelte 5 + Runes (`$state`, `$derived`, `$effect`) best practices | Building or optimizing Svelte components |
| [`sveltekit-structure`](skills/sveltekit-structure/SKILL.md) | SvelteKit routing, layouts, error boundaries, SSR, hydration | Any SvelteKit file structure or routing question |
| [`nextjs-react-expert`](skills/nextjs-react-expert/SKILL.md) | React + Next.js performance: bundle size, waterfalls, server/client components | React/Next.js performance optimization |
| [`frontend-design`](skills/frontend-design/SKILL.md) | Design thinking for web UI: colors, typography, animation, UX psychology | Designing components, color schemes, layouts |
| [`tailwind-patterns`](skills/tailwind-patterns/SKILL.md) | Tailwind CSS v4 patterns: CSS-first config, container queries, design tokens | Styling with Tailwind |

### Backend

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [`nodejs-best-practices`](skills/nodejs-best-practices/SKILL.md) | Node.js: framework selection, async patterns, security, architecture | Node.js server development |
| [`python-patterns`](skills/python-patterns/SKILL.md) | Python: framework selection, async, type hints, project structure | Python application development |
| [`fastapi-python`](skills/fastapi-python/SKILL.md) | FastAPI best practices for async APIs | Building REST APIs with FastAPI |
| [`api-patterns`](skills/api-patterns/SKILL.md) | REST vs GraphQL vs tRPC, versioning, pagination, response formats | API design decisions |

### Database

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [`database-design`](skills/database-design/SKILL.md) | Schema design, indexing strategy, ORM selection, serverless databases | Any database design or migration task |
| [`graph-database-expert`](skills/graph-database-expert/SKILL.md) | Graph modeling, traversals, query optimization, SurrealDB specialist | Graph schema design or graph query optimization |
| [`neo4j-cypher-skill`](skills/neo4j-cypher-skill/SKILL.md) | Generates and optimizes Cypher 25 queries for Neo4j 2025.x/2026.x | Writing or tuning Neo4j Cypher queries |

### Testing & Quality

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [`testing-patterns`](skills/testing-patterns/SKILL.md) | Unit, integration, and mocking strategies | Writing any type of test |
| [`tdd-workflow`](skills/tdd-workflow/SKILL.md) | RED-GREEN-REFACTOR cycle for Test-Driven Development | Implementing features test-first |
| [`webapp-testing`](skills/webapp-testing/SKILL.md) | E2E testing with Playwright, deep audit strategies | End-to-end or browser automation tests |
| [`code-review-checklist`](skills/code-review-checklist/SKILL.md) | Code quality, security, and best practice review checklist | PR reviews and code audits |
| [`lint-and-validate`](skills/lint-and-validate/SKILL.md) | Automatic linting, formatting, and static analysis after code changes | After every code modification |

### DevOps & Security

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [`deployment-procedures`](skills/deployment-procedures/SKILL.md) | Safe deployment workflows, rollback strategies, verification | Production deployments |
| [`vulnerability-scanner`](skills/vulnerability-scanner/SKILL.md) | OWASP 2025, supply chain security, attack surface mapping | Security audits and vulnerability reviews |

### Specialized Tools

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [`mcp-builder`](skills/mcp-builder/SKILL.md) | MCP (Model Context Protocol) server design: tool patterns, resource patterns | Building MCP integrations |
| [`i18n-localization`](skills/i18n-localization/SKILL.md) | Detecting hardcoded strings, managing translation files, RTL support | Internationalizing an application |
| [`performance-profiling`](skills/performance-profiling/SKILL.md) | Profiling, measurement, and optimization techniques | Diagnosing performance bottlenecks |
| [`systematic-debugging`](skills/systematic-debugging/SKILL.md) | 4-phase root cause analysis with evidence-based verification | Complex or production bugs |
| [`documentation-templates`](skills/documentation-templates/SKILL.md) | README, API docs, code comments, and AI-friendly documentation templates | Writing any technical documentation |

---

## Agents

Agents are specialist personas. Each agent has a curated list of skills it loads and a `description` that tells the LLM when to invoke it. Triggers (keywords) are listed in the agent's frontmatter `description` field.

| Agent | Role | Auto-trigger Keywords | Skills Loaded |
|-------|------|-----------------------|---------------|
| [`orchestrator`](agents/orchestrator.md) | Multi-agent coordinator for complex tasks | complex, multi-domain, full-stack | `parallel-agents`, `behavioral-modes`, `plan-writing`, `architecture` + more |
| [`backend-specialist`](agents/backend-specialist.md) | Node.js, Python, serverless, APIs, auth | backend, server, api, endpoint, database, auth | `nodejs-best-practices`, `python-patterns`, `api-patterns`, `database-design` + more |
| [`frontend-specialist`](agents/frontend-specialist.md) | Svelte/React, styling, state management | component, svelte, react, ui, ux, css, tailwind, responsive | `svelte-expert`, `sveltekit-structure`, `tailwind-patterns`, `nextjs-react-expert` |
| [`database-architect`](agents/database-architect.md) | Schema design, queries, migrations, serverless DBs | database, sql, schema, migration, query, postgres, index, table | `database-design`, `graph-database-expert`, `neo4j-cypher-skill` |
| [`security-auditor`](agents/security-auditor.md) | OWASP 2025, zero trust, supply chain security | security, vulnerability, owasp, xss, injection, auth, encrypt, pentest | `vulnerability-scanner`, `api-patterns` |
| [`test-engineer`](agents/test-engineer.md) | TDD, test automation, coverage | test, spec, coverage, jest, pytest, playwright, e2e, unit test | `testing-patterns`, `tdd-workflow`, `webapp-testing`, `code-review-checklist` |
| [`devops-engineer`](agents/devops-engineer.md) | Deployment, CI/CD, server ops (⚠️ high risk) | deploy, production, server, pm2, ssh, release, rollback, ci/cd | `deployment-procedures` |
| [`debugger`](agents/debugger.md) | Root cause analysis, crash investigation | bug, error, crash, not working, broken, investigate, fix | `systematic-debugging` |
| [`performance-optimizer`](agents/performance-optimizer.md) | Speed, bundle size, Core Web Vitals | performance, optimize, speed, slow, memory, cpu, benchmark, lighthouse | `performance-profiling` |
| [`explorer-agent`](agents/explorer-agent.md) | Codebase discovery, architectural audits, research | audit, explore, analyze repo, refactor plan, investigate | `architecture`, `plan-writing`, `brainstorming`, `systematic-debugging` |
| [`product-owner`](agents/product-owner.md) | Requirements, roadmaps, backlog prioritization | requirements, user story, backlog, MVP, PRD, stakeholder | `plan-writing`, `brainstorming`, `grill-me` |
| [`project-planner`](agents/project-planner.md) | Task breakdown, file structure, dependency graphs | new project, plan feature, project structure | `app-builder`, `plan-writing`, `brainstorming` |
| [`documentation-writer`](agents/documentation-writer.md) | README, API docs, changelogs | readme, api docs, changelog, documentation | `documentation-templates`, `i18n-localization`, `write-a-skill` |
| [`code-archaeologist`](agents/code-archaeologist.md) | Legacy code, reverse engineering, modernization | legacy, refactor, spaghetti code, analyze repo, explain codebase | `clean-code`, `code-review-checklist` |

### How to Invoke an Agent

Agents are selected automatically by the `intelligent-routing` skill. You can also invoke them explicitly:

```
@backend-specialist add a rate limiter to the Express app
@security-auditor review the authentication flow
@test-engineer write unit tests for the user service
```

---

## Workflows (Slash Commands)

Workflows are slash commands that trigger predefined sequences of agents and skills.

| Command | Description | What It Does |
|---------|-------------|--------------|
| [`/create`](workflows/create.md) | Start a new application | Triggers `app-builder` skill + interactive dialogue to scaffold a full project |
| [`/enhance`](workflows/enhance.md) | Add features to an existing app | Loads session state, understands current stack, iterates with `app-builder` |
| [`/plan`](workflows/plan.md) | Generate a project plan (no code) | Invokes `project-planner` agent, runs Socratic gate, writes a plan file |
| [`/brainstorm`](workflows/brainstorm.md) | Structured idea exploration | Activates BRAINSTORM mode, explores multiple options before any implementation |
| [`/debug`](workflows/debug.md) | Systematic bug investigation | Activates DEBUG mode with `systematic-debugging` skill |
| [`/test`](workflows/test.md) | Generate and run tests | Creates tests with `tdd-workflow`/`testing-patterns`, then executes them |
| [`/deploy`](workflows/deploy.md) | Production deployment wizard | Pre-flight checks → deployment → verification via `deployment-procedures` |
| [`/orchestrate`](workflows/orchestrate.md) | Explicit multi-agent coordination (≥3 agents) | Forces orchestration mode for complex multi-domain tasks |
| [`/preview`](workflows/preview.md) | Manage local dev server | Start, stop, or check the status of the preview server |
| [`/status`](workflows/status.md) | Show project and agent status | Displays session info, tech stack, current features, and active agents |
| [`/ui-ux-pro-max`](workflows/ui-ux-pro-max.md) | AI-powered design system | 50+ styles, 97 color palettes, 57 font pairings, 99 UX guidelines |

### Quick Reference

```bash
/create a SvelteKit e-commerce app with Stripe
/enhance add dark mode to the dashboard
/plan build a real-time chat feature
/brainstorm authentication strategies for a multi-tenant SaaS
/debug login returns 401 intermittently
/test the user registration flow
/deploy to production
/orchestrate redesign the entire auth system
/preview start
/status
```

---

## Scripts

Python utilities located in `scripts/` for automation and state management.

| Script | Description |
|--------|-------------|
| [`session_manager.py`](scripts/session_manager.py) | Analyzes project state: detects tech stack, tracks files, provides session summary. Used by `/status` and `/enhance`. |
| [`auto_preview.py`](scripts/auto_preview.py) | Manages the local dev server lifecycle for `/preview`. |
| [`checklist.py`](scripts/checklist.py) | Tracks task checklist state across agent turns. |
| [`verify_all.py`](scripts/verify_all.py) | Runs all verification steps (lint, type-check, tests) in one pass. |

**Usage example:**

```bash
python .agent/scripts/session_manager.py info
python .agent/scripts/verify_all.py
```

---

## Usage Tips

### 1. Load `intelligent-routing` in your system prompt

Add `intelligent-routing` to your agent configuration so the LLM automatically picks the right specialist without explicit commands:

```yaml
skills: intelligent-routing, clean-code, behavioral-modes
```

The LLM will then silently route `"fix the login bug"` to `debugger` and `"add a dark mode toggle"` to `frontend-specialist`.

### 2. Always start with `brainstorming` for complex tasks

Before any multi-step implementation, triggering `brainstorming` prevents wasted effort by surfacing missing requirements early.

### 3. Use `behavioral-modes` to switch gears

```
Enter BRAINSTORM mode - let's explore options for the new notification system
Enter IMPLEMENT mode - build the notification service
Enter REVIEW mode - check the code I just wrote
```

### 4. Use `caveman` mode to reduce token usage

If responses are too long or you're burning through context:

```
caveman mode on
```

The LLM will drop filler words while keeping full technical accuracy.

### 5. Chain workflows for a full feature cycle

```
/plan the feature → /brainstorm edge cases → /create (or /enhance) → /test → /deploy
```

### 6. Override auto-routing when needed

```
@database-architect  // forces database-architect even if routing would choose something else
```

---

## Getting Started

Copy [`BOOTSTRAP.md`](BOOTSTRAP.md) into your project as `GEMINI.md` or `CLAUDE.md` and fill in the `<PLACEHOLDERS>` to wire the framework into your AI assistant in seconds.

The [`SKILLS_INDEX.json`](SKILLS_INDEX.json) at the repository root is a machine-readable manifest of all skills — use it for programmatic routing, tooling, or to quickly survey available capabilities without opening individual `SKILL.md` files.
