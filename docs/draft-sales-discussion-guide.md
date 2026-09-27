# Draft — Sales discussion guide

> **Status:** Temporary draft. Use with [draft-product-concept-and-packaging.md](./draft-product-concept-and-packaging.md).

---

## 1. Qualify: is this sellable to them?

| Question | Good fit if… |
|----------|----------------|
| Do you route/classify **operational** items (tickets, lines, messages)? | Yes — core use case |
| Can you pass a **structured snapshot** (`state`) into an API? | Yes — Observe contract |
| Do you need **audit** of why a decision happened? | Hybrid profile + per-question probs |
| Are rules **partially** fuzzy (wording, tone, category)? | Judge value |
| Are some rules **exact** (caps, IDs)? | Policies + code story |
| Can they run **Docker/on-prem** or WSL stack? | Technical fit |
| Who owns **improvement** after go-live? | Agent + eval loop = ongoing value |

**Poor fit:** need full vault product, no engineering, expect 100% accuracy with zero fixtures, cloud-only mandate with no local option.

---

## 2. Discovery script (30 min)

1. **Domain** — “What artifact is in `state`? What actions follow?”  
2. **Today** — Rules engine? LLM prompts? Manual queue?  
3. **Pain** — False escalations? Missed compliance? Slow new domains?  
4. **Proof** — “How do you know v2 is better than v1?” → **eval** hook  
5. **Deployment** — SaaS vs on-prem; data residency  
6. **Buyer** — Platform vs line-of-business vs compliance  

Capture: candidate **profile_id**, 3 example `state` lines, success criteria.

---

## 3. Value props by persona

| Persona | Lead with |
|---------|-----------|
| **VP Engineering** | Versioned profiles, MCP, API, local Ollaya |
| **Product / Ops** | Playground, demos, outcome routing narrative |
| **Compliance** | Deterministic policies + explainable Judge + eval reports |
| **AI lead** | Not another chatbot—**typed** probabilities, fixture harness |

---

## 4. Objection handling (draft)

| Objection | Response |
|-----------|----------|
| “We already use GPT.” | Profiles are **versioned rubrics** + eval; GPT is opaque. |
| “Accuracy too low.” | Show expense-demo **76%** + improvement loop; start with assist not full auto-Act. |
| “Who builds profiles?” | Profile agent + your SME; we professional-services Tier C. |
| “Act/routing?” | You own orchestrator; we document thresholds; ontology outcomes align. |
| “Lock-in?” | YAML in git; open stack; Postgres export via `get_profile`. |

---

## 5. Packaging conversation

Present **Tier A–D** from product draft. Ask:

- Embed only (A)?  
- Analysts in Playground (B)?  
- Many new domains / agent (C)?  
- CI gates on eval % (D)?

**Pilot proposal (template):**

- 1 profile, 10 fixtures, baseline eval, 2 improvement iterations, publish to their Postgres.  
- Success: match rate ≥ X% on agreed cases + SME sign-off on explain samples.

---

## 6. Proof assets to show

| Asset | Path |
|-------|------|
| Mental model | `Doc/judgment-loop-generic.jpg` |
| Live demos | `Demo/triage`, `time-reporting`, `expense-demo` |
| Eval gaps (honest) | `Demo/expense-demo/eval-gaps.md` |
| Agent flow | `AGENTS.md`, `Doc/draft-agent-eval-and-improvement.md` |
| Stack | `docker-compose.yml`, Playground :5173 |

---

## 7. After the call — internal

- [ ] Fit score (1–5)  
- [ ] Recommended tier  
- [ ] Pilot profile domain  
- [ ] Engineering prerequisites  
- [ ] Competitive note  

---

## 8. Terms to avoid / prefer

| Avoid (ambiguous) | Prefer |
|-------------------|--------|
| “AI decides everything” | “Judgment profile + your policies” |
| “Trains the model” | “Improves rubrics and fixtures” |
| “RAG included” | “Vault merges into `state`—you operate retrieval” |
