# Contributing to Skill Vault

Thank you for helping build Skill Vault — Wolven's organized, browsable library of AI agent **skills** and **advisor personas**.

Start at the [root README](README.md) for catalog orientation, pre-launch status, and links to each domain index. This guide covers how to author, place, and review **catalog** entries. It consolidates standards from the metadata contract, taxonomy, templates, and security expectations for V1 scaffolding and session 2 marketplace curation.

## Catalog scope

Skill Vault's **product** is catalog skills and agents under [`catalog/`](catalog/). They are governed, taxonomy-placed, and intended for adoption in agent runtimes (Cursor, Claude, Codex, and others).

| Surface | Location | Role |
|---------|----------|------|
| **Catalog product** | `catalog/<domain>/skills/`, `catalog/<domain>/agents/` | Vault skills and agents — browse, adopt, contribute via PR |
| **Dev-time tooling** | `.agents/`, `.compozy/` (gitignored) | Compozy `cy-*` pipeline, council agents, and harness used to **build and maintain** this repo |

**Catalog skills live under `catalog/`, not `.agents/`.** Dev-time skills under `.agents/skills/` and agents under `.compozy/` are internal tooling. They must not be listed in domain indexes, cross-linked from catalog entries as product skills, or placed under `catalog/` without a deliberate migration PR.

V1 is **scaffolding only** — taxonomy, empty domain indexes, metadata standards, and templates. Marketplace curation in **session 2** populates the catalog before go-live.

## Before you start

| Resource | Purpose |
|----------|---------|
| [README.md](README.md) | Catalog hub — orientation, domain overview, catalog vs dev boundary |
| [`catalog/taxonomy.yaml`](catalog/taxonomy.yaml) | Authoritative domain and subgroup hierarchy |
| [`docs/metadata-contract.md`](docs/metadata-contract.md) | OKF-light frontmatter specification |
| [`catalog/templates/skill/SKILL.md`](catalog/templates/skill/SKILL.md) | Skill authoring template |
| [`catalog/templates/agent/AGENT.md`](catalog/templates/agent/AGENT.md) | Agent authoring template |

Copy the appropriate template into the target domain folder, fill in OKF-light frontmatter, and update the domain index when adding entries (session 2 onward).

## Taxonomy placement rules

Physical placement uses **flat domain folders** plus **metadata-driven subgroups**. Subgroup is expressed in `tags`, not in the directory path.

### Path conventions

| Entry type | Path pattern |
|------------|--------------|
| Skill | `catalog/<domain>/skills/<skill-name>/SKILL.md` |
| Agent | `catalog/<domain>/agents/<agent-name>/AGENT.md` |

Where `<domain>` is a top-level domain id from [`catalog/taxonomy.yaml`](catalog/taxonomy.yaml): `engineering`, `marketing`, `product`, or `ops`.

### Choosing domain and subgroup

1. Open [`catalog/taxonomy.yaml`](catalog/taxonomy.yaml) and pick the **domain** that best matches the skill or agent's audience and purpose.
2. Pick the **subgroup** within that domain whose title and description fit the entry.
3. Place the file under `catalog/<domain>/skills/` or `catalog/<domain>/agents/` per the path table above.
4. Add the subgroup **`id`** (not the title) to the entry's `tags` list.

**Subgroup tag rule:** Every catalog entry **must** include its domain subgroup `id` as one of the `tags` values. Additional tags are optional.

Example — a Compozy workflow skill in engineering:

```yaml
tags:
  - compozy    # required subgroup id from taxonomy.yaml
  - workflow   # optional
```

Valid subgroup ids for V1:

| Domain | Subgroup ids |
|--------|--------------|
| `engineering` | `compozy`, `development`, `qa` |
| `marketing` | `content`, `campaigns`, `analytics` |
| `product` | `discovery`, `planning` |
| `ops` | `workflows`, `tooling` |

If no subgroup fits, open a separate PR to extend [`catalog/taxonomy.yaml`](catalog/taxonomy.yaml) and the matching domain [`index.md`](catalog/engineering/index.md) before adding the entry. Do not invent tag values that are not defined in the taxonomy.

### Updating navigation

When catalog entries exist (session 2+), append a row to the flat **Skills** or **Agents** table in `catalog/<domain>/index.md` (ADR-004). Each row includes Title (linked), Description, and Subgroup column derived from entry `tags`. Do not use per-subgroup section headings for entry listings.

## PR review checklist

V1 has no automated metadata validator (ADR-007). Reviewers enforce standards manually on every catalog PR. Use this checklist:

### Metadata (OKF-light)

- [ ] Entry is under `catalog/`, not `.agents/` or `.compozy/`
- [ ] `type` is `Skill` or `Agent`
- [ ] `title` and `description` are present and suitable for index listings
- [ ] `tags` is a non-empty list that includes a **valid subgroup id** for the entry's domain (per [`catalog/taxonomy.yaml`](catalog/taxonomy.yaml) and [`docs/metadata-contract.md`](docs/metadata-contract.md))
- [ ] Skills include `name` (lowercase, hyphen-separated); agents do not require `name`
- [ ] Frontmatter matches [`docs/metadata-contract.md`](docs/metadata-contract.md)

### Paths and placement

- [ ] File path follows `catalog/<domain>/skills/<name>/SKILL.md` or `catalog/<domain>/agents/<name>/AGENT.md`
- [ ] Domain in the path matches the chosen taxonomy domain
- [ ] **Catalog vs dev path separation:** no dev harness files moved into `catalog/` without explicit migration; no catalog index links to `.agents/` or `.compozy/` paths as product entries

### Cross-links

- [ ] Links between catalog skills and agents use **relative markdown paths** (see [Cross-link convention](#cross-link-convention))
- [ ] Link targets exist under `catalog/` and use `SKILL.md` or `AGENT.md` as appropriate

### Navigation and taxonomy sync

- [ ] Domain `index.md` updated when adding or removing entries (session 2+)
- [ ] Flat index table row added with Title, Description, and Subgroup column matching entry `tags` (ADR-004)
- [ ] Subgroup column uses comma-separated subgroup ids when entry has multiple subgroup tags

### Session 2 pairing metadata (ADR-006)

- [ ] Paired agents include `related_skills` listing relative paths to paired `SKILL.md` files
- [ ] Skills with paired agents include `related_agents` when reverse navigation is intended
- [ ] Optional `links.yaml` sidecar uses relative paths and valid `relations` schema when present
- [ ] Primary pairings live in front matter; `links.yaml` holds richer typed edges only when needed

### Session 2 import hygiene (ADR-005, ADR-003)

- [ ] Partial-pick imports contain only roster-listed files — no full upstream folder copy
- [ ] Skill/agent bodies remain market-default — no vault-specific navigation embeds in bodies

### Security (when applicable)

- [ ] If the skill bundles scripts, recommends package installs, or modifies code/deps, Snyk audit expectations were followed (see [Security audit (Snyk)](#security-audit-snyk))
- [ ] Critical and high Snyk findings are remediated or explicitly documented before merge

## Cross-link convention

Related catalog skills and agents should link to each other with relative markdown links from the referencing file's location.

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

Use paths relative to the current file so links work in GitHub, local clones, and static exports. Full field-level metadata rules are in [`docs/metadata-contract.md`](docs/metadata-contract.md).

## Security audit (Snyk)

Per [ADR-008](.compozy/tasks/skill-vault-foundation/adrs/adr-008.md), catalog and dev skills that touch **application source code** or **dependency manifests** must be security-reviewed with Snyk. Snyk complements manual PR review; it does not validate OKF-light frontmatter or taxonomy placement.

### When Snyk applies

Run Snyk when a catalog skill (or its bundled assets):

- Modifies or generates application source code
- Adds, upgrades, or recommends dependencies (`package.json`, `go.mod`, `requirements.txt`, `pom.xml`, lockfiles, etc.)
- Ships scripts or manifests imported from an external marketplace

Markdown-only documentation changes do **not** require Snyk scans.

### MCP workflow (preferred)

When the Snyk Secure Development plugin and MCP server are available in the agent runtime:

1. **Snyk Code (SAST):** Run `snyk_code_scan` on changed source paths using the workspace **absolute path**.
2. **Snyk SCA:** When manifest or lockfiles change, run `snyk_sca_scan` with the workspace absolute path (`all_projects: true` when appropriate).
3. **New packages:** Use the `secure-dependency-health-check` skill before selecting dependencies.
4. **Remediation:** Resolve or document **critical** and **high** findings before merge. Re-run scans after fixes.

The [skill template](catalog/templates/skill/SKILL.md) includes a **Security Audit (Snyk)** section agents should follow when executing code- or dependency-changing workflows.

### Manual security review fallback

When Snyk MCP is unavailable (no plugin, no authentication, or offline runtime):

1. **Reviewer** inspects bundled scripts and manifest files for obvious risk (eval, `curl | bash`, unpinned remote deps, secrets in repo).
2. **Importer** documents skipped Snyk scans and rationale in the PR description.
3. **Maintainer** runs Snyk locally or in a Snyk-enabled environment before merge when the change touches code or dependencies.
4. Do not merge high-risk imports solely on markdown review — escalate or defer until Snyk or equivalent review is possible.

Session 2 marketplace imports **must** be reviewed for security posture; importers run Snyk on any bundled scripts or manifest files before merge when MCP is available.

## Private overlay repository

Company-specific catalog skills (internal workflows, proprietary tooling, private integrations) belong in a **private overlay repo**, not in the public Skill Vault OSS tree.

### Clone-and-merge pattern

1. **Fork or clone** the public Skill Vault repository (or maintain a private fork with the same `catalog/` layout).
2. **Create a private overlay repo** that mirrors the catalog structure: `catalog/<domain>/skills/`, `catalog/<domain>/agents/`, and optionally a private `catalog/taxonomy.yaml` extension.
3. **Add company entries** under the overlay using the same OKF-light metadata, subgroup tags, and path conventions documented here.
4. **Merge upstream** public Skill Vault changes periodically (taxonomy updates, template improvements, contribution guide) into the overlay to stay compatible.
5. **Install or copy** catalog paths from the overlay into agent runtimes the same way as public catalog skills — overlay paths are additive, not replacements for the OSS catalog unless your team configures that.

No multi-repo tooling ships in V1. Teams manage overlay sync with standard git remotes, subtrees, or manual merge workflows. Keep private skills out of public PRs to the OSS repo.

## Session 2 marketplace import workflow

Session 2 is the pre-launch curation pass that populates the empty catalog shell. High-level workflow:

1. **Select sources** — Curate from marketplaces such as [skill.fish](https://www.skill.fish/), Tessl, [skills.sh](https://skills.sh/), Vercel marketplace skills, and other major agent skill directories. Prioritize deep review of [tech-leads-club/agent-skills](https://github.com/tech-leads-club/agent-skills); skip low-value groupings per curator judgment.
2. **Evaluate fit** — Decide domain, subgroup, and whether the skill belongs in the public catalog or a private overlay.
3. **Normalize metadata** — Apply OKF-light frontmatter per [`docs/metadata-contract.md`](docs/metadata-contract.md); include the subgroup id in `tags`. Start from [`catalog/templates/skill/SKILL.md`](catalog/templates/skill/SKILL.md) or [`catalog/templates/agent/AGENT.md`](catalog/templates/agent/AGENT.md).
4. **Place files** — Copy into `catalog/<domain>/skills/<name>/` or `catalog/<domain>/agents/<name>/` per [Taxonomy placement rules](#taxonomy-placement-rules).
5. **Security review** — Run Snyk Code/SCA on bundled scripts and manifests when present; follow [manual fallback](#manual-security-review-fallback) if MCP is unavailable.
6. **Update navigation** — Append a flat index table row in `catalog/<domain>/index.md` with Subgroup column (ADR-004); add pairing via front matter `related_*` and optional `links.yaml` (ADR-006).
7. **Open PR** — Request review using the [PR review checklist](#pr-review-checklist). Iterate until metadata, placement, links, and security expectations pass.

**Go-live gate (session 2):** Coverage-driven launch acceptance — verify metrics M1–M8 before removing README pre-launch status:

| Metric | Criterion |
|--------|-----------|
| M1 | ≥2 of 3 engineering subgroups (`compozy`, `development`, `qa`) populated in entry `tags` |
| M2 | ≥2 of 3 marketing subgroups (`content`, `campaigns`, `analytics`) populated |
| M3 | MVP slots imported or documented deferral (`verificacao`/`verifier` deferred) |
| M4 | 100% code-bearing imports Snyk-clean (0 unremediated critical/high) |
| M5 | 100% OKF-light metadata compliance via extended checklist |
| M6 | Reviewer link-graph assessment for paired entries |
| M7 | Obsidian smoke test — wiki-links resolve at repo root |
| M8 | ≥80% of catalog entries in engineering + marketing domains |

Product and ops domains may remain thin. Public launch waits until M1–M8 pass.

## Authoring templates

| Template | Path | Use for |
|----------|------|---------|
| Skill | [`catalog/templates/skill/SKILL.md`](catalog/templates/skill/SKILL.md) | New catalog skills — includes OKF-light frontmatter and Security Audit (Snyk) section |
| Agent | [`catalog/templates/agent/AGENT.md`](catalog/templates/agent/AGENT.md) | New catalog advisor personas — includes OKF-light frontmatter and related-skill link pattern |

Copy the template, replace placeholder frontmatter and body sections, and place the result under the correct domain folder.

## Questions

- **Catalog orientation and domains** — [README.md](README.md)
- **Frontmatter fields and examples** — [`docs/metadata-contract.md`](docs/metadata-contract.md)
- **Domain and subgroup ids** — [`catalog/taxonomy.yaml`](catalog/taxonomy.yaml)
- **Architecture decisions** — [`.compozy/tasks/skill-vault-foundation/adrs/`](.compozy/tasks/skill-vault-foundation/adrs/)
