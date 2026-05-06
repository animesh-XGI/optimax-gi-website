# OptimaX Agent Model Governance & Cost Management Policy

**Version:** 1.0  
**Effective:** May 6, 2026  
**Owner:** Board / Human Operator  
**Location:** `docs/05_ARCHITECTURE/`

---

## 1. Purpose & Background

This policy governs how AI models are assigned to OptimaX agents, who has authority to change them, and how we manage AI operational costs.

It was established following the **OPT-57 incident (May 6, 2026)**, where a cost-reduction request caused the CEO agent to issue a blanket model-change policy using an invalid model ID (`claude-haiku-4-6`). This cascaded across the entire team, causing all agent runs to fail simultaneously.

---

## 2. Agent Model Assignments (Canonical)

Authorized model assignments as of May 6, 2026. These are the **CANONICAL** defaults — do not deviate without appropriate authority (see Section 4).

| Agent | Role | AI Model | Tier | Rationale |
|---|---|---|---|---|
| CEO | Strategic Leader | `claude-opus-4-7` | Premium | Highest reasoning for strategy & governance |
| CTO | Technical Lead | `claude-sonnet-4-6` | Standard | Strong reasoning for architecture & code review |
| Engineer | Implementation | `claude-sonnet-4-6` | Standard | Reliable for dev tasks, debugging, PRs |
| IT Support Lead | Support Ops | `claude-haiku-4-5` | Economy | High-volume routine tasks, low cost priority |
| System Admin | Infrastructure | `claude-haiku-4-5` | Economy | High-volume infra ops, low cost priority |

---

## 3. Valid Anthropic Model IDs (as of May 2026)

Only use verified Anthropic model IDs. Using invalid model IDs will cause all agent runs to fail.

- `claude-haiku-4-5` or `claude-haiku-4-5-20251001`
- `claude-sonnet-4-6`
- `claude-opus-4-6`
- `claude-opus-4-7`

> **DO NOT use:** `claude-haiku-4-6` — this model does not exist and caused the OPT-57 incident.

---

## 4. Model Change Governance Rules

### Rule 1 — Self-Model Lock
Your AI model is fixed. You are **NOT authorized to change your own model**.

### Rule 2 — Peer/Subordinate Model Changes
Another agent's model can be changed by their **manager or a higher-authority agent**. The change must use a valid Anthropic model ID and align with the role tier guidelines above.

### Rule 3 — No Blanket Policy Changes
Agents must **NOT** issue a policy instruction like "all agents should use model X" without explicit approval from the human operator (Board/Owner). Such changes can cascade and break all agents simultaneously.

### Rule 4 — Validate Before Apply
Before changing any agent model, verify the model ID exists and is accessible. Reference Section 3 (Valid Model IDs) in this document. A single invalid ID will cause all runs for that agent to fail.

### Rule 5 — Managed in Routine (no Board escalation required)
Model assignments within the approved tier for a role are a **routine operations matter**. Managers handle this in their regular cadence without escalating to the Board. Cross-tier changes (e.g., moving CEO from Opus to Haiku) **DO require** Board/human approval.

---

## 5. Cost Management Guidelines

### Model Tiers and Approximate Relative Cost

| Tier | Models | Relative Cost | Use For |
|---|---|---|---|
| Premium | Opus | ~10x base | CEO-level strategic tasks requiring highest reasoning |
| Standard | Sonnet | ~3x base | CTO/Engineer level tasks with complex reasoning |
| Economy | Haiku | ~1x base | High-volume, routine, low-complexity tasks |

### Cost Control Triggers

- If **daily AI spend exceeds $10**: Review which agents are running the most tasks.
- If **monthly spend jumps >50%** vs prior month: Investigate new tasks assigned to premium-tier agents.
- **Never** assign Sonnet or Opus to agents performing repetitive infra/support tasks.

> **Lesson from OPT-57:** A cost spike from $5 to $28 in 15 minutes is a signal of runaway tasks on expensive models. Haiku for IT Support Lead and System Admin is the intended cost control.

---

## 6. Incident Record: OPT-57 (May 6, 2026)

- **Trigger:** Human operator requested cost optimization. CEO (OPT-57) responded by creating policy to set all agents to `claude-haiku-4-6`.
- **Impact:** All agent runs failed. Tasks OPT-50, OPT-60, OPT-63 blocked.
- **Fix Applied:** Models corrected to valid IDs per the canonical table in Section 2. Failed tasks retried. This policy document created.

---

## 7. References

- OPT-57: Cost Optimization for Agents (origin issue)
- OPT-58: CTO review of transition issues
- OPT-65: Append AI Model Governance Rules to all agent AGENTS.md files
- [Anthropic Model Reference](https://platform.claude.com/docs/about-claude/models/overview)
- Paperclip Agent Config UI: Settings > Configuration > Model
