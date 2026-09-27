# Draft — Agent eval & continuous improvement loops

> **Status:** Temporary draft for internal alignment. Not customer-facing copy.  
> **Skills:** `nextforge-profile-agent`, `judgment-eval-and-fixtures`, `simple-judgment-mental-model`  
> **MCP:** `run_harness_eval`, `try_profile`, `analyze_judgment_improvement`

---

## 1. What the profile agent does (end-to-end)

```text
Context in
  → Mental model decomposition (Profile Discovery)
  → Ontology + vault/policies (Define)
  → Questions T1→T4 (Judge instruments)
  → validate → [publish to Postgres]
  → Fixtures + harness eval
  → Explain output + gaps + recommendations
  → Apply YAML/ontology fixes → re-eval (reinforcement loop)
  → optional publish
```

| Phase | Agent feature | Primary artifacts |
|-------|---------------|-------------------|
| Orient | `list_profiles`, spec load | `preset_id` |
| Discover | Map context → ontology, vault, Judge plan | Profile Discovery brief |
| Author | Ontology + questions YAML | `domains/`, `questions/`, Postgres |
| Validate | `validate_ontology_yaml`, `validate_questions_yaml` | Gate before publish |
| Publish | `publish_profile` | Same DB as Playground |
| **Eval** | Fixtures + `run_harness_eval` | `fixtures/<preset>-cases.json`, reports |
| **Explain** | Scenario → per-question reading + probabilities | Chat / playbook |
| **Recommend** | Ranked fixes (questions, ontology, policies, fixtures, Act) | `eval-gaps.md` |
| **Reinforce** | Apply edits, re-run eval, track match % | Iteration until bar met |

**No publish required for eval** — harness uses local lab `questions/*.yml` + Ollaya.

---

## 2. Judgment task layers (design order)

When a spec implies multiple “judgment tasks,” design in layers (one Ollaya decide call; split **questions**, not vague compound nouls):

| Layer | Purpose | Example (`expense-demo`) |
|-------|---------|---------------------------|
| **T1 Situation** | Facts from `state` | `is_business` |
| **T2 Classification** | Bucket / type | `category` choice |
| **T3 Gates** | Policy / evidence | `receipt_provided` |
| **T4 Next action** | Escalate / approve | `manager_review`, `spend_level` |
| **T5 Hypotheses** (rare) | Competing interpretations | Only if product needs explicit alternates |

---

## 3. Eval loop (quality & coverage)

### 3.1 Create test cases

- **8–12 fixtures** per profile (`laya-local-lab/fixtures/<preset>-cases.json`).
- Each case: `id`, `note`, `state`, `expect` { question_id → yes/no/label }.
- **Coverage matrix:** happy path, each choice branch, each thresholded noul yes+no, spec success criteria, adversarial vagueness.
- Demo mirror: `Demo/<preset>/eval-cases.json`, gap write-up `Demo/<preset>/eval-gaps.md`.

### 3.2 Run eval

```bash
cd nextforge-decision-server/laya-local-lab
npm run eval -- <preset>
```

MCP: `run_harness_eval` with `preset_name`.

**Metrics:** cases run, expect match rate, per-question accuracy table, miss list.

### 3.3 Explain (single scenario or miss)

After `try_profile` or from eval row:

- Plain-language **reading** per question.
- **Numbers:** noul → yes/no @ 0.5; choice label + confidence; score.
- **Signal:** confident | **borderline** (e.g. noul 0.4–0.6) | wrong | low choice confidence.

MCP prompt: **`analyze_judgment_improvement`** (`state`, optional `try_result_json`, `run_eval`).

### 3.4 Recommend (improvement backlog)

Ranked changes:

| Area | Examples |
|------|----------|
| **Questions** | Criteria examples, split nouls, instruction anchors to `state` |
| **Ontology** | New `state` fields, `outcomes`, `planned_questions`, `open_questions` |
| **Policies** | `deterministic: true` for exact math/IDs |
| **Fixtures** | New branch coverage |
| **Spec** | Fix `expect` or `domain-spec.md` |
| **Act** | Orchestrator thresholds (app layer; document in spec) |

Gap types: Judge-instrument, Judge-calibration, Coverage, Constrain, Act, Spec.

### 3.5 Apply & re-verify

1. User approves proposed diffs.  
2. `validate_*` → edit lab YAML / ontology.  
3. Re-run eval; update gap doc baseline (date, %).  
4. `publish_profile` when shipping to shared Postgres/Playground.

---

## 4. Reinforcement / improvement loop (product narrative)

Maps to mental model **Feedback & learn**:

```text
Observe (fixtures = realistic states)
  → Judge (eval measures question quality)
  → Act (you change profile + routing)
  → Learn (gaps doc + metrics history)
  → back to Define / Judge authoring
```

| Reinforcement signal | What improves |
|----------------------|---------------|
| Eval **miss** | Question instructions, criteria, splits |
| **Borderline** probabilities | Instruments, policies, don’t auto-act |
| **Coverage hole** | New fixture + ontology scenario |
| **Act routing** mismatch (Judge ok) | Thresholds in orchestrator, document in ontology |
| Repeat eval **↑ match %** | Profile “trained” in engineering sense (rubrics, not model weights) |

**Not in scope unless requested:** Ollaya fine-tune / modelfile calibration (document only).

---

## 5. Runtime vs authoring (sales-safe clarity)

| Loop step | In Postgres profile? | Who runs it today |
|-----------|----------------------|-------------------|
| Observe | `state` contract | Customer app |
| Constrain / Bound | `policies`, `outcomes` | App / harness |
| **Judge** | `questions_yaml` | **`try_profile`** / decide API |
| Act | Documented outcomes | Customer orchestrator |

NextForge **packages** the judgment **profile** + **agent** to author and **prove** it with eval—not a full BPM replacement.

---

## 6. Reference implementation (`expense-demo`)

| Item | Location |
|------|----------|
| 10-case fixture | `laya-local-lab/fixtures/expense-demo-cases.json` |
| Baseline gaps | `Demo/expense-demo/eval-gaps.md` (~76% 22/29 expects) |
| Weakest question | `manager_review` ~60% |

Use as demo story: eval → explain Uber miss → recommend travel criteria + receipt wording.

---

## 7. Agent entry prompts (internal)

```text
Decompose context with mental model → Profile Discovery → build YAML →
validate → [publish] → fixtures → run_harness_eval → eval-gaps.md with recommendations →
ask to apply fixes and re-eval.
```

```text
analyze_judgment_improvement: expense-demo + state line + explain low probs + recommend.
```

---

## 8. Open doc tasks

- [ ] Customer-facing eval report PDF template  
- [ ] SLA / match-rate targets per industry vertical  
- [ ] Integration story for Act layer (reference orchestrator)  
- [ ] Rename “reinforcement” in UI if sales prefers “continuous improvement” or “governance loop”
