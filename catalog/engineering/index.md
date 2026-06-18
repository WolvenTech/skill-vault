# Engineering

Skills and advisor personas for software delivery — workflows, development practices, and quality assurance. This domain index is the **GitHub-primary browse surface** for engineering catalog entries (ADR-004).

Subgroup ids are sourced from [`catalog/taxonomy.yaml`](../taxonomy.yaml). Catalog entries express subgroup placement via OKF-light `tags` (see [`docs/metadata-contract.md`](../../docs/metadata-contract.md)).

| Subgroup id | Title |
|-------------|-------|
| `compozy` | Compozy Workflows |
| `development` | Development |
| `qa` | Quality Assurance |

## Skills

| Title | Description | Subgroup |
|-------|-------------|----------|
| [TLC Spec Driven](skills/tlc-spec-driven/SKILL.md) | Project and feature planning with 4 adaptive phases - Specify, Design, Tasks, Execute. Auto-sizes depth by complexity... | `compozy` |
| [Coding Guidelines](skills/coding-guidelines/SKILL.md) | Behavioral guidelines to reduce common LLM coding mistakes. Use when writing, modifying, or reviewing code — implemen... | `development` |
| [Security Best Practices](skills/security-best-practices/SKILL.md) | Perform language and framework specific security best-practice reviews and suggest improvements. Use when the user ex... | `development`, `qa` |
| [Playwright Skill](skills/playwright-skill/SKILL.md) | Complete browser automation with Playwright. Auto-detects dev servers, writes clean test scripts to /tmp. Test pages,... | `qa` |
| [Create ADR](skills/create-adr/SKILL.md) | Creates Architecture Decision Records (ADRs) to document significant architectural choices and their rationale for fu... | `development` |
| [Create RFC](skills/create-rfc/SKILL.md) | Creates structured Request for Comments (RFC) documents for proposing and deciding on significant changes. Use when t... | `development` |
| [Create Technical Design Doc](skills/create-technical-design-doc/SKILL.md) | Creates comprehensive Technical Design Documents (TDD) with mandatory and optional sections through interactive disco... | `development` |
| [Docs Writer](skills/docs-writer/SKILL.md) | Write, review, and edit documentation files with consistent structure, tone, and technical accuracy. Use when creatin... | `development` |
| [Codenavi](skills/codenavi/SKILL.md) | Your pathfinder for navigating unknown codebases. Investigates with precision, implements surgically, and never assum... | `development` |
| [GitHub Address Comments](skills/gh-address-comments/SKILL.md) | Address review and issue comments on the open GitHub PR for the current branch using gh CLI. Use when user says "addr... | `development` |
| [Frontend Design](skills/frontend-design/SKILL.md) | Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks ... | `development` |
| [Domain Analysis](skills/domain-analysis/SKILL.md) | Maps business domains and suggests service boundaries in any codebase using DDD Strategic Design. Use when asking "wh... | `development` |
| [Modular Decomposition](skills/modular-decomposition/SKILL.md) | Runs a sequenced monolith-to-modular pipeline that sizes and inventories components, finds shared domain duplication,... | `development` |
| [Coupling Analysis](skills/coupling-analysis/SKILL.md) | Analyzes coupling between modules using the three-dimensional model (strength, distance, volatility) from "Balancing ... | `development` |
| [React Composition Patterns](skills/react-composition-patterns/SKILL.md) | React composition patterns that scale. Use when refactoring components with boolean prop proliferation, building flex... | `development` |
| [Decomposition Planning Roadmap](skills/decomposition-planning-roadmap/SKILL.md) | Creates step-by-step decomposition plans and migration roadmaps for breaking apart monolithic applications. Use when ... | `development` |
| [Tactical DDD](skills/tactical-ddd/SKILL.md) | Detects anemic domain models, validates and refactors them into rich domain models, and enforces tactical DDD pattern... | `development` |
| [React Best Practices](skills/react-best-practices/SKILL.md) | React and Next.js performance optimization guidelines from Vercel Engineering. Use when writing, reviewing, or refact... | `qa` |
| [Web Accessibility](skills/web-accessibility/SKILL.md) | Audit and improve web accessibility following WCAG 2.1 guidelines. Use when asked to "improve accessibility", "a11y a... | `qa` |
| [Web Best Practices](skills/web-best-practices/SKILL.md) | Apply modern web development best practices for security, compatibility, and code quality. Use when asked to "apply b... | `qa` |
| [SEO](skills/seo/SKILL.md) | Optimize for search engine visibility and ranking. Use when asked to "improve SEO", "optimize for search", "fix meta ... | `qa` |
| [Security Threat Model](skills/security-threat-model/SKILL.md) | Repository-grounded threat modeling that enumerates trust boundaries, assets, attacker capabilities, abuse paths, and... | `development` |
| [Core Web Vitals](skills/core-web-vitals/SKILL.md) | Optimize Core Web Vitals (LCP, INP, CLS) for better page experience and search ranking. Use when asked to "improve Co... | `qa` |
| [Perf Lighthouse](skills/perf-lighthouse/SKILL.md) | 'Run Lighthouse audits locally via CLI or Node API, parse and interpret reports, and set performance budgets. Use whe... | `qa` |
| [Web Design Guidelines](skills/web-design-guidelines/SKILL.md) | Review UI code for Web Interface Guidelines compliance. Use when asked to "review my UI", "check accessibility", "aud... | `qa` |
| [GitHub Fix CI](skills/gh-fix-ci/SKILL.md) | Use when a user asks to debug or fix failing GitHub PR checks that run in GitHub Actions. Uses `gh` to inspect checks... | `development`, `qa` |
| [Chrome DevTools](skills/chrome-devtools/SKILL.md) | Browser debugging, performance profiling, and automation via Chrome DevTools MCP. Use when user says "debug this page... | `qa` |
| [Vercel Deploy](skills/vercel-deploy/SKILL.md) | Deploy applications and websites to Vercel. Use when the user requests deployment actions like "deploy my app", "depl... | `development` |
| [Mermaid Studio](skills/mermaid-studio/SKILL.md) | Expert Mermaid diagram creation, validation, and rendering with dual-engine output (SVG/PNG/ASCII). Supports all 20+ ... | `development` |
| [Frontend Blueprint](skills/frontend-blueprint/SKILL.md) | AI frontend specialist and design consultant that guides users through a structured discovery process before generati... | `development` |
| [Modular Design Principles](skills/modular-design-principles/SKILL.md) | Technology-agnostic guidance for modular systems — bounded contexts, clear boundaries, composability, state isolation, e... | `development` |

Skills live under [`skills/`](skills/).

## Agents

| Title | Description | Subgroup |
|-------|-------------|----------|


Agents live under [`agents/`](agents/).
