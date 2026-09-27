# Draft — Product concept & packaging (NextForge)

> **Status:** Temporary draft for product/site/sales exploration.  
> **Audience:** Founders, product, sales prep—not final marketing.

---

## 1. One-sentence pitch (working)

**NextForge** helps teams **define, publish, and prove** local **judgment profiles**—ontology + probabilistic questions—that turn operational **state** into **actions**, with an **AI agent** that decomposes specs, runs **eval**, and recommends **continuous improvement** without cloud model lock-in (Ollaya local).

---

## 2. Problem we address

| Pain | Today | NextForge angle |
|------|--------|-----------------|
| Rules + ML don’t share one contract | Spreadsheets + ad-hoc prompts | **Profile** = ontology + questions + policies in one versioned bundle |
| “Can we trust the model on case X?” | Manual spot checks | **Fixture eval** + match rate + per-question accuracy |
| Prompt drift | Undocumented changes | Git lab files + Postgres publish + validate gates |
| Compliance / audit | Black-box LLM only | **Hybrid:** deterministic policies + **explainable** question answers |
| New domain slow | Weeks of prompt tuning | **Profile agent:** spec → discovery → YAML → try/eval loop |

---

## 3. Core product objects (sellable units)

| Object | What buyer gets | Analogy |
|--------|-----------------|--------|
| **Decision profile** | `ontology_yaml` + `questions_yaml` + `id` | Sheet music + solo part |
| **Judgment runtime** | Ollaya decide on `state` (local) | Performance |
| **Profile agent** | Cursor/MCP authoring + eval + recommendations | Composer + rehearsal coach |
| **Playground** | Edit YAML, publish, try | Studio |
| **Harness eval** | Regression on fixtures | QA suite for judgment |

**Not the product (today):** full case management UI, knowledge vault product, enterprise BPM—**integrate** via `state` in / API out.

---

## 4. Mental model (buyer-friendly)

**Context:** Ontology (structure) + Knowledge vault (rules)—authored in profile.

**Loop per decision:**

```text
Observe → Constrain → Bound → Judge → Act → Learn
```

NextForge **ships** Define + Judge instruments; customer **runs** Observe/Act; we **prove** Judge with eval.

Diagrams: `Doc/judgment-loop-generic.jpg`, time-reporting example.

---

## 5. Packaging options (draft tiers)

Use for sales conversations—numbers TBD.

### Tier A — **Profile Runtime** (technical buyer)

- Ollaya + nextforge-server + Postgres profiles  
- REST/MCP: list, get, publish, try, delete  
- Self-hosted (Docker Compose)  
- **Buyer:** platform team embedding decide API  

### Tier B — **Profile Studio** (+ Playground)

- Everything in A + YAML editors, publish to DB, try UI  
- **Buyer:** product ops, business analysts with technical ally  

### Tier C — **Profile Agent** (+ authoring intelligence)

- MCP agent: discovery, validate, eval, gaps, recommendations  
- Skills: mental model, eval fixtures, improvement playbook  
- **Buyer:** teams shipping **new domains** monthly  

### Tier D — **Governance / CI** (future packaging)

- Harness eval in CI, match-rate gates, report archive  
- **Buyer:** regulated ops (time, expenses, triage)  

**Bundle narrative:** “Author with Agent (C), operate with Studio (B), embed with Runtime (A), govern with Eval CI (D).”

---

## 6. Differentiation (draft)

| vs | NextForge |
|----|-----------|
| Raw LLM prompts | Versioned **profiles**, validate gates, fixture eval |
| Pure rules engine | **Probabilistic** judgment where spec is fuzzy |
| Cloud-only AI platforms | **Local** Ollaya + sovereign deploy story |
| Generic MLOps | **Domain judgment** ontology + question types (choice/score/noul) |

---

## 7. Site / concept blocks (initial IA)

**Home**

- Hero: “Judgment profiles you can prove.”  
- Loop animation: Observe → … → Learn.  
- CTA: See demos (triage, time-reporting, expense-demo).

**Product**

- Profiles · Agent · Eval · Playground · MCP  
- Hybrid rules + model diagram.

**How it works**

- 3 steps: Define profile → Run on state → Improve with eval.

**Demos**

- Three vertical snippets + eval scorecard screenshot.

**Developers**

- Compose up, MCP config, API table.

**Trust**

- Local inference, no training data leave box (when deployed on-prem).

*(Draft only—no copy finalized.)*

---

## 8. Demo storyline for sales (15 min)

1. **Problem:** expense line routing—receipt, category, manager.  
2. **Profile:** show ontology outcomes + 5 questions.  
3. **Try:** one line in Playground or `try_profile`.  
4. **Eval:** 10 cases, 76%—honest about gaps.  
5. **Improve:** Uber case → recommend criteria fix → “this is the loop.”  
6. **Deploy:** same profile in Postgres; their app sends `state`.

---

## 9. What we need from sales (discovery questions)

See [draft-sales-discussion-guide.md](./draft-sales-discussion-guide.md).

---

## 10. Risks / honesty for sellability

| Risk | Mitigation story |
|------|------------------|
| Act not in box | Document thresholds; partner services; roadmap orchestrator SDK |
| Eval is lab-first | Postgres try for prod smoke; same questions after publish |
| Agent needs Cursor/dev | MCP + docs; services engagement for Tier C |
| Model quality ceiling | Eval + rubric iteration; deterministic policies for hard rules |

---

## 11. Glossary (packaging language)

| Term | Meaning |
|------|---------|
| Profile | Versioned judgment bundle |
| Judge | Probabilistic questions on `state` |
| Eval | Fixture regression for Judge |
| Improvement loop | Explain → recommend → fix → re-eval |
| Profile agent | MCP/Cursor agent implementing full lifecycle |
