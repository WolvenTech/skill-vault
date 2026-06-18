---
name: example-skill
type: Skill
title: Example Skill
description: One-line summary for index listings and search snippets.
tags:
  - compozy
  - workflow
---

# Example Skill

Replace the frontmatter values and body sections below when authoring a catalog skill. Copy this template to `catalog/<domain>/skills/<skill-name>/SKILL.md` and include a subgroup id from [`catalog/taxonomy.yaml`](../../taxonomy.yaml) in `tags`.

## Overview

Describe what this skill helps agents accomplish, when to apply it, and the expected outcome. Keep this section concise — one or two short paragraphs.

## Instructions

Document the workflow steps agents should follow when this skill is invoked.

1. **Gather context** — List inputs, files, or prerequisites the agent needs before starting.
2. **Execute** — Describe the main steps in order. Use sub-bullets for branching or optional paths.
3. **Validate** — State how the agent confirms the work is complete and correct.
4. **Hand off** — Note any artifacts, follow-up tasks, or related catalog entries to reference.

Add optional sections as needed (e.g., error handling, examples, related skills) using relative markdown links between catalog entries.

## Security Audit (Snyk)

When this skill modifies application code or adds dependencies:

1. Run Snyk Code (`snyk_code_scan`) on changed source paths using the workspace absolute path.
2. Run Snyk SCA (`snyk_sca_scan`) when manifest files change.
3. Use the `secure-dependency-health-check` skill before selecting new packages.
4. Remediate critical/high findings before recommending the workflow.
