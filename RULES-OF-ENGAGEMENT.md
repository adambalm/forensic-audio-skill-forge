# Rules of Engagement

**Engagement:** Forensic Audio Skill Forge
**Pattern:** MDX-Net/VR Centrifuge
**Date Initiated:** 2026-01-10

---

## Overview

This document establishes the rules governing collaboration in this Skill Forge engagement. All participating agents (GA, IA) and the Human Orchestrator (HO) are bound by these rules.

**Read order for new agents:**
1. This document (RULES-OF-ENGAGEMENT.md)
2. `protocols/lanesborough-protocol.md` - Role definitions and gate structure
3. `protocols/black-flag-protocol.md` - Epistemic hygiene requirements
4. `protocols/skill-forge-pattern.md` - The deliberation process
5. `CONTEXT.md` - Technical environment and constraints
6. `dialogue/001-initialization.md` - Your first task

---

## Role Assignments

| Role | Agent | Function | Transport |
|------|-------|----------|-----------|
| **Human Orchestrator (HO)** | Ed O'Connell | Final Approval / Gatekeeper | GitHub commits |
| **Generalizing AI (GA)** | Claude Code (Opus 4.5) | Solution Architect / Implementer | GitHub commits |
| **Inspecting AI (IA)** | Gemini 1.5 Pro | Forensic Auditor / Schema Enforcer | Manual paste to GitHub |

**Heterogeneity note:** Gemini's multimodal video/audio analysis capabilities are critical for this engagement. GA cannot replicate IA's forensic auditing of source material.

---

## Protocol Stack

This engagement is governed by three interlocking protocols:

### 1. Lanesborough Protocol (Primary)
*See: `protocols/lanesborough-protocol.md`*

Governs the structure of collaboration:
- **Phases:** Initiation → Proposal → Refinement Loop → Escalation → Execution
- **Gates:** Understanding Gate (UG), Agreement Gate (AG), Articulation Gate
- **Turn markers:** Each exchange prefixed with `=== HANDSHAKE TURN N (agent) ===`
- **Logging:** All decisions logged with timestamp, author, and effect

### 2. Black Flag Protocol (Epistemic Hygiene)
*See: `protocols/black-flag-protocol.md`*

Governs how claims are made and verified:
- **Clause 2:** Verify Before Assert - if you can check it, check it
- **Clause 4.1:** Infrastructure Proposal Gate - query existing inventory before proposing new tools
- **Clause 6:** State Your Confidence - accompany claims with certainty level
- **Clause 11:** Multi-Agent Consistency - no agent claims another's work
- **Clauses 15-17:** Temporal validity checks (from Temporal Validity Protocol)

**Verification markers:**
| Marker | Meaning |
|--------|---------|
| `[verified]` | Independently confirmed |
| `[contradicts: X]` | Understanding differs from X |
| `[cannot verify: Y]` | Lacks access to verify |
| `[unverifiable: judgment call]` | No verification procedure exists |
| `[certified by HO, DATE]` | Human certified after articulating |

### 3. Skill Forge Pattern (Process)
*See: `protocols/skill-forge-pattern.md`*

Governs the deliberation process:
- **Goal:** Qualified human judgment, NOT AI consensus
- **Paraphrase is adversarial:** Each model treats the other's output as suspect
- **Human articulation gate:** HO must restate decisions before approving
- **Amortization:** Resulting skill is reusable for future similar problems

---

## Gate Status

| Gate | Status | Notes |
|------|--------|-------|
| Understanding Gate | **OPEN** | GA and IA must establish shared understanding |
| Agreement Gate | **OPEN** | Not yet addressed |
| Articulation Gate | **OPEN** | HO has not yet articulated core decision |

---

## Dialogue Protocol

### File Naming
```
dialogue/
├── 001-initialization.md      # Opening prompt for IA
├── 002-ia-response.md         # IA's first response
├── 003-ga-response.md         # GA's response to IA
├── 004-ia-response.md         # IA's next response
└── ...
```

### Required Structure

Each dialogue file MUST include:

```markdown
# [Turn Type]: [Brief Description]

**Turn:** [N]
**Author:** [GA | IA | HO]
**Timestamp:** [ISO 8601]
**Gate Status:** [UG: OPEN/CLOSED] [AG: OPEN/CLOSED]

---

[Content]

---

## Verification Summary

| Claim | Status |
|-------|--------|
| [claim 1] | [verified/contradicts/cannot verify/unverifiable] |
| ... | ... |

## Open Questions

- [Any unresolved items]
```

### Turn Taking

1. IA reads GA proposal
2. IA paraphrases AND flags each claim with verification status
3. GA responds to all flags (defend, concede, or acknowledge)
4. Repeat until Understanding Gate closes
5. Then proceed to substantive critique and Agreement Gate

### Escalation

After **3 passes** without convergence on any gate:
- Surface open questions to HO
- HO may certify, decide, or request continued iteration

---

## Commitments

### GA Commits To:
- [ ] Black Flag epistemic hygiene (verify before assert)
- [ ] Temporal validity checks on all cited documents
- [ ] Responding to ALL IA verification flags
- [ ] Not claiming IA's work as own

### IA Commits To:
- [ ] Adversarial paraphrase (not passive restatement)
- [ ] Flagging every claim with verification status
- [ ] Treating GA output as potentially hallucinated
- [ ] Surfacing failure modes and edge cases

### HO Commits To:
- [ ] Articulating decisions before approving
- [ ] Certifying only claims they can restate
- [ ] Logging all gate approvals
- [ ] Intervening on impasse

---

## Success Criteria

This Skill Forge succeeds when:

1. **Understanding Gate closes** - GA and IA have established shared technical understanding
2. **Agreement Gate closes** - Executable plan with verified claims
3. **HO articulates** - Ed can restate the core decision in his own words
4. **Skill is captured** - `artifacts/INSTRUCTIONS.md` contains reusable forensic audio recovery skill
5. **Audio is recovered** - The "E-D-M-O-N-D" sequence is intelligible in final output

---

## Failure Modes to Avoid

From Skill Forge anti-patterns:
- **Passive paraphrase** - IA must actively verify, not just restate
- **Rubber-stamping** - HO must articulate before approving
- **Homogeneous models** - We use Claude + Gemini specifically for swiss cheese coverage
- **Not capturing the skill** - Deliberation cost must be amortized

---

*This document is binding for all participants. Violations are logged as protocol breaches.*
