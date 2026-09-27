# NextForge documentation

## Core mental model

| Document | Purpose |
|----------|---------|
| [simple-judgment-mental-model.md](./simple-judgment-mental-model.md) | Generic loop + NextForge mapping + **reverse map** (agent vs runtime) |
| [judgment-loop-generic.jpg](./judgment-loop-generic.jpg) | **Generic** diagram (all domains) |
| [judgment-loop-time-reporting.jpg](./judgment-loop-time-reporting.jpg) | **Example** — `time-reporting` profile |

**Agent skill:** `simple-judgment-mental-model` · MCP `nextforge://skills/simple-judgment-mental-model`

---

## Draft notes — agent, eval, improvement (internal)

> Temporary drafts for product, sales, and site concepts. Not final customer copy.

| Draft | Purpose |
|-------|---------|
| [draft-agent-eval-and-improvement.md](./draft-agent-eval-and-improvement.md) | Full agent pipeline: discovery → build → **eval** → explain → **recommend** → re-run |
| [draft-reinforcement-loop.md](./draft-reinforcement-loop.md) | **Feedback & learn** as rubric reinforcement; metrics; site snippet |
| [draft-product-concept-and-packaging.md](./draft-product-concept-and-packaging.md) | Product definition, tiers A–D, differentiation, site IA |
| [draft-sales-discussion-guide.md](./draft-sales-discussion-guide.md) | Qualification, discovery script, objections, pilot template |

**Implementation skills (repo):**

- `nextforge-profile-agent` — systematic build + eval suite  
- `judgment-eval-and-fixtures` — fixtures, coverage, gaps, improvement playbook  
- MCP: `run_harness_eval`, `try_profile`, `analyze_judgment_improvement`

**Naming (display vs slugs):** [../NAMING.md](../NAMING.md)

---

## Related (application repo)

Demos, `AGENTS.md`, Cursor rules, and lab fixtures live in the **NextForge application** monorepo (not in this community bundle).
