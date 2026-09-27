# NextForge — agent & skill naming (canonical)

Display names for sales, docs, and Cursor rules. **Technical slugs** stay stable in the application repo.

## Primary agent

| Role | Display name | Technical ID |
|------|--------------|--------------|
| Cursor / MCP agent | **Profile Forge** | Skill `nextforge-profile-agent` · prompt `nextforge_profile_agent` |
| MCP server | *(product)* **NextForge** | namespace `nextforge` |

## Core skills (order)

| Order | Display name | Technical slug |
|-------|--------------|----------------|
| 0 | **Judgment Loop** | `simple-judgment-mental-model` |
| 1 | **Profile Forge** | `nextforge-profile-agent` |
| 2 | **Prove & Improve** | `judgment-eval-and-fixtures` |

**Stack line:** `Judgment Loop → Profile Forge → Prove & Improve`

## Workflow phases

| Phase | Label | Action |
|-------|-------|--------|
| 0 | Orient | Mental model + list profiles |
| 1 | Discover | Profile discovery brief |
| 2 | Define | Ontology YAML |
| 3 | Instrument | Questions YAML (T1→T4) |
| 4 | Ship | Publish (when requested) |
| 5 | Prove | Harness eval + gaps doc |
| 6 | Improve | Recommendations → re-eval |

## Supporting skills (on demand)

| Display name | Technical slug |
|--------------|----------------|
| Ontology Sketch | `light-ontology-from-spec` |
| Question Craft | `probabilistic-question-design` |
| Question Lifecycle | `ollaya-question-lifecycle` |
| Profile Ops | `nextforge-profiles` |
| Lab Runbook | `laya-local-lab` |
| Ollaya Runbook | `ollaya-local-runbook` |

## MCP prompt aliases (docs only)

| Alias | Prompt |
|-------|--------|
| forge | `nextforge_profile_agent` |
| improve | `analyze_judgment_improvement` |
| ontology | `build_ontology_from_spec` |
| questions | `design_questions` |
| profiles | `manage_profiles` |
| lifecycle | `facilitate_question_lifecycle` |

## Product tiers (draft)

| Tier | Name | Emphasis |
|------|------|----------|
| A | Runtime | API + local decide |
| B | Studio | Playground + Profile Ops |
| C | Profile Forge | Full skill trio + MCP agent |
| D | Governance | Eval CI + Improve loop |
