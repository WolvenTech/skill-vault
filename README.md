# Skill Vault

Wolven's organized, browsable library of AI agent **skills** and **advisor personas** — the canonical place where teams find vetted workflows instead of reinventing prompts.

Catalog skills and agents live under [`catalog/`](catalog/). They are the **product** of this repository: governed, taxonomy-placed, and intended for adoption in agent runtimes (Cursor, Claude, Codex, and others).

You can open this repository as an **Obsidian vault** at the repo root for graph view and wiki-link navigation across catalog entries.

## Pre-launch status

**Session 2 curation complete.** Engineering and marketing domains are populated with curated skills and agents. Browse by domain below or open this repository as an Obsidian vault at the repo root for graph navigation.

## Catalog vs dev-time tooling

| Surface | Location | Purpose |
|---------|----------|---------|
| **Catalog product** | [`catalog/`](catalog/) | Vault skills and agents — browse, adopt, contribute via PR |
| **Dev-time tooling** | `.agents/`, `.compozy/` (gitignored) | Compozy `cy-*` pipeline, council agents, and harness used to **build and maintain** this repo |

Skills under `.agents/` and agents under `.compozy/` are **not** catalog entries. They do not appear in domain indexes and are not part of the Skill Vault product surface.

## Browse by domain

The catalog is organized into four top-level domains. Each domain has an index page listing subgroups (from [`catalog/taxonomy.yaml`](catalog/taxonomy.yaml)) and sections for skills and agents.

| Domain | Focus | Index |
|--------|-------|-------|
| **Engineering** | Software delivery — workflows, development practices, quality assurance | [catalog/engineering/index.md](catalog/engineering/index.md) |
| **Marketing** | Go-to-market — content, campaigns, analytics | [catalog/marketing/index.md](catalog/marketing/index.md) |
| **Product** | Product work — discovery and planning | [catalog/product/index.md](catalog/product/index.md) |
| **Operations** | Operational workflows and platform tooling | [catalog/ops/index.md](catalog/ops/index.md) |

## For contributors

- **Taxonomy** — [`catalog/taxonomy.yaml`](catalog/taxonomy.yaml) defines domains and subgroups.
- **Templates** — [`catalog/templates/skill/SKILL.md`](catalog/templates/skill/SKILL.md) and [`catalog/templates/agent/AGENT.md`](catalog/templates/agent/AGENT.md) for authoring.
- **Metadata** — [`docs/metadata-contract.md`](docs/metadata-contract.md) documents OKF-light frontmatter for catalog entries.

Contribution guide and placement rules: [`CONTRIBUTING.md`](CONTRIBUTING.md).
