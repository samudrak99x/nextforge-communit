# Draft — Reinforcement & improvement loop (product concept)

> **Status:** Temporary draft. Links mental model **Feedback & learn** to agent **eval + recommend** features.

---

## 1. Name in product language

| Internal | Customer-facing options |
|----------|-------------------------|
| Reinforcement loop | **Continuous improvement loop** |
| Phase 6 iteration | **Profile governance** |
| Eval re-run | **Judgment regression** |

Pick one term for sales deck; keep “reinforcement” in engineering docs if useful.

---

## 2. Loop diagram

```text
                    ┌─────────────────┐
                    │ Define profile  │
                    │ ontology + Qs   │
                    └────────┬────────┘
                             │
         ┌───────────────────┼───────────────────┐
         ▼                   ▼                   ▼
   ┌───────────┐      ┌────────────┐      ┌─────────────┐
   │ Fixtures  │      │  Publish   │      │  Production │
   │ (coverage)│      │ (optional) │      │  try/state  │
   └─────┬─────┘      └────────────┘      └──────┬──────┘
         │                                         │
         ▼                                         │
   ┌───────────┐                                   │
   │ Harness   │◄──────────────────────────────────┘
   │ eval      │         misses / borderline in prod
   └─────┬─────┘
         ▼
   ┌───────────┐
   │ Explain   │  scenario → probabilities → intent
   └─────┬─────┘
         ▼
   ┌───────────┐
   │ Recommend │  questions · ontology · policies · fixtures
   └─────┬─────┘
         ▼
   ┌───────────┐
   │ Apply     │  validate YAML → re-eval
   └─────┬─────┘
         │
         └──────────► (metrics ↑) ──► back to Define
```

---

## 3. Reinforcement signals

| Signal | Source | Agent action |
|--------|--------|--------------|
| Expect **miss** | `run_harness_eval` | Recommend instrument fix; add fixture |
| **Borderline** prob | `try_profile` | Warn on auto-Act; split noul |
| **Coverage** gap | Matrix vs spec | New case + ontology note |
| **New scenario** in prod | User report | Profile Discovery delta |
| **Match rate** trend | Serial eval reports | Track in `eval-gaps.md` baselines |

---

## 4. What gets “reinforced”

| Artifact | Not reinforced (out of scope) |
|----------|-------------------------------|
| Question instructions & criteria | Base model weights (unless fine-tune project) |
| Ontology `state` / `outcomes` / `policies` | |
| Fixture library | |
| Act threshold documentation | |
| Domain spec | |

This is **rubric reinforcement**, not RL training—important for sales accuracy.

---

## 5. Agent features mapped to loop

| Loop stage | MCP / skill |
|------------|-------------|
| Eval | `run_harness_eval`, `judgment-eval-and-fixtures` |
| Explain + recommend | `analyze_judgment_improvement`, `eval-improvement-playbook.md` |
| Apply | `validate_*`, edit YAML, `publish_profile` |
| Measure | Reports in `laya-local-lab/reports/` |

---

## 6. Metrics for packaging (proposal)

| Metric | Definition |
|--------|------------|
| **Case pass rate** | expects matched / total expects |
| **Per-question accuracy** | from harness report |
| **Coverage** | % planned branches with ≥1 fixture |
| **Borderline rate** | cases with any noul in 0.4–0.6 (manual count) |

Pilot SLO example: “≥85% case pass rate on agreed fixture set after 2 improvement iterations.”

---

## 7. Site snippet (draft copy)

> **Prove, then improve.** Every judgment profile ships with eval fixtures and a clear scorecard. When reality drifts, the Profile Agent explains misses, recommends rubric and policy updates, and re-runs regression—so your routing logic stays accountable without rewriting prompts in the dark.

---

## 8. Related docs

- [draft-agent-eval-and-improvement.md](./draft-agent-eval-and-improvement.md)  
- [simple-judgment-mental-model.md](./simple-judgment-mental-model.md)  
- [Demo/expense-demo/eval-gaps.md](../Demo/expense-demo/eval-gaps.md)
