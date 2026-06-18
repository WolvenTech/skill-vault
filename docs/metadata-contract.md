# OKF-light Metadata Contract

Every catalog skill and agent in Skill Vault must include YAML frontmatter that conforms to this contract. The contract is the import standard for marketplace curation and the baseline for PR review (ADR-007: manual PR-review validation in V1).

This document specifies **catalog** metadata only. Dev-time skills under `.agents/` and `.compozy/` follow a separate convention and are not catalog entries.

## OKF-light fields (all entries)

All catalog entries — both Skills and Agents — **must** include these frontmatter fields:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `type` | string | **Yes** | Entry kind: `Skill` or `Agent` |
| `title` | string | **Yes** | Human-readable name shown in domain indexes and browse views |
| `description` | string | **Yes** | One-line summary for index listings and search snippets |
| `tags` | list of strings | **Yes** | Classification tags; must include the entry's subgroup id (see [Subgroup tag placement](#subgroup-tag-placement)) |

These fields form the OKF-light subset used for metadata interchange. Additional OKF fields are optional in V1.

### Skill-only field

Skills additionally require the Agent Skills baseline field:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | **Yes** (Skills only) | Machine identifier for the skill; lowercase, hyphen-separated (e.g. `compozy-advisor`) |

Agents do **not** require `name`. The `title` field serves as the human-facing identifier for agents.

## Required vs optional summary

| Field | Skill | Agent |
|-------|-------|-------|
| `type` | Required | Required |
| `title` | Required | Required |
| `description` | Required | Required |
| `tags` | Required | Required |
| `name` | Required | Not used |
| Other OKF fields | Optional | Optional |

## Subgroup tag placement

Subgroup placement is **metadata-driven**, not folder-driven. Physical paths use flat domain folders (`catalog/<domain>/skills/` or `catalog/<domain>/agents/`); subgroups are expressed through tags.

**Rule:** Every catalog entry **must** include its domain subgroup `id` as one of the `tags` values.

The authoritative list of domain and subgroup ids is [`catalog/taxonomy.yaml`](../catalog/taxonomy.yaml). Valid subgroup ids for V1:

| Domain | Subgroup ids |
|--------|--------------|
| `engineering` | `compozy`, `development`, `qa` |
| `marketing` | `content`, `campaigns`, `analytics` |
| `product` | `discovery`, `planning` |
| `ops` | `workflows`, `tooling` |

Additional tags beyond the required subgroup id are optional (e.g. `workflow`, `automation`).

### Examples

**Skill in engineering / compozy:**

```yaml
---
name: compozy-pipeline
type: Skill
title: Compozy Pipeline
description: Run Compozy PRD tasks end-to-end with verification.
tags:
  - compozy
  - workflow
---
```

**Agent in engineering / compozy:**

```yaml
---
type: Agent
title: Compozy Advisor
description: Guides Compozy workflow setup and task execution.
tags:
  - compozy
---
```

**Skill in marketing / content:**

```yaml
---
name: blog-outline
type: Skill
title: Blog Outline Generator
description: Produce structured outlines from a brief.
tags:
  - content
  - writing
---
```

If a tag value does not match a subgroup id defined in `catalog/taxonomy.yaml` for the entry's domain, reviewers should reject the PR until the tag is corrected or the taxonomy is updated via a separate PR.

## File path conventions

Catalog entries live under domain folders. The file name and directory structure follow the Agent Skills open format.

| Entry type | Path pattern |
|------------|--------------|
| Skill | `catalog/<domain>/skills/<skill-name>/SKILL.md` |
| Agent | `catalog/<domain>/agents/<agent-name>/AGENT.md` |

Where:

- `<domain>` is a top-level domain id from `catalog/taxonomy.yaml` (`engineering`, `marketing`, `product`, or `ops`).
- `<skill-name>` and `<agent-name>` are lowercase, hyphen-separated directory names (typically aligned with the skill's `name` field or the agent's slugified `title`).

Examples:

- `catalog/engineering/skills/compozy-pipeline/SKILL.md`
- `catalog/engineering/agents/compozy-advisor/AGENT.md`
- `catalog/marketing/skills/blog-outline/SKILL.md`

Subgroup is **not** reflected in the path. Use `tags` and the domain index page to associate entries with subgroups.

## Cross-link convention

Related catalog skills and agents should link to each other using **relative markdown links** from the referencing file's location.

Pattern:

```markdown
[Link text](../<type-plural>/<entry-name>/<ENTRY-FILE>.md)
```

Examples from `catalog/engineering/skills/compozy-pipeline/SKILL.md`:

```markdown
See also the [Compozy Advisor](../agents/compozy-advisor/AGENT.md) for workflow design.
```

Examples from `catalog/engineering/agents/compozy-advisor/AGENT.md`:

```markdown
Pair with [Compozy Pipeline](../skills/compozy-pipeline/SKILL.md) for task execution.
```

Use paths relative to the current file so links work in GitHub, local clones, and static exports without rewriting. Full placement and PR checklist details appear in `CONTRIBUTING.md` (authored separately).

## Catalog vs dev-time skill metadata

Skill Vault maintains two distinct skill locations:

| Location | Purpose | Metadata |
|----------|---------|----------|
| `catalog/<domain>/skills/` and `catalog/<domain>/agents/` | **Product** — browsable vault skills and advisor personas | OKF-light contract (this document) |
| `.agents/skills/` and `.compozy/` | **Dev harness** — repository build, PRD pipeline, and maintainer tooling | Agent Skills `name` + `description`; no OKF-light `type`/`tags` requirement |

Dev-time skills (e.g. `cy-execute-task`, `cy-final-verify`) are gitignored or treated as internal tooling. They must **not** be listed as catalog product entries or cross-linked from catalog indexes as if they were vault skills.

When importing or authoring **catalog** content, always apply this contract. When editing **dev** skills, follow the Agent Skills format used elsewhere under `.agents/skills/` — do not add catalog `type` or subgroup `tags` unless migrating content into the catalog.

## Enforcement

V1 has no automated metadata validator. Reviewers enforce this contract manually during PR review (ADR-007). Checklist items:

1. All required OKF-light fields present (`type`, `title`, `description`, `tags`).
2. Skills include `name`.
3. `tags` includes a valid subgroup id from `catalog/taxonomy.yaml` for the entry's domain.
4. File path matches the conventions above.
5. Cross-links use relative paths between catalog entries.
6. Entry is under `catalog/`, not `.agents/` or `.compozy/`.

## References

- [`catalog/taxonomy.yaml`](../catalog/taxonomy.yaml) — authoritative domain and subgroup ids
- ADR-006 — YAML taxonomy with metadata-driven subgroup placement
- ADR-007 — Manual PR-review validation for V1
