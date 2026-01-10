# The Lanesborough Protocol

*Finalized Specification - September 2025*

---

## Purpose

The Lanesborough Protocol governs collaboration between human and AI agents in multi-step workflows. It ensures clarity, recoverability, accountability, and convergence toward auditable outcomes.

---

## Roles

### Human Orchestrator (HO)
- Defines high-level goals.
- Sets iteration limits.
- Grants final execution approval.
- Intervenes in case of impasse.

### Generalizing AI (GA)
- Architect role.
- Produces high-level proposals, abstractions, and plans.
- Issues tasks/questions to the IA.

### Inspecting AI (IA)
- Ground-truth role.
- Paraphrases GA proposals, challenges them, and validates against concrete details.
- Executes tests and records decisions in the log.

---

## Protocol Phases

### 1. Initiation
- **Actor:** HO
- **Action:** States the goal and sets the maximum number of refinement iterations.

### 2. Proposal
- **Actor:** GA
- **Action:** Produces the initial high-level plan or architectural approach.
- **Output:** Must be specific enough for IA to test and refine.

### 3. Refinement Loop
- **Actor:** GA and IA alternate turns.
- **Process:**
  1. **Mirror and Counter (IA):** IA paraphrases GA proposal, offers critique or alternative.
  2. **Refine and Re-task (GA):** GA accepts/corrects IA understanding, adjusts plan.
  3. **Closure Condition (Handshake):** One agent issues Summary of Agreement + "Agreed." Partner replies "Agreed."

- **Exit:** Loop continues until handshake or max iterations.

### 4. Escalation
- **If successful handshake:** Last AI requests HO approval to execute.
- **If impasse (max iterations reached):** IA reports impasse and requests HO intervention.

### 5. Execution and Logging
- **Actor:** IA
- **Action:** Upon HO approval, IA executes or records the decision.
- **Mandatory Logging:** Append to log with timestamp, decision, GA/IA contributions.

---

## Exception Handling
- **Actor:** IA
- **Trigger:** If IA cannot complete a task (error, missing file, failed test).
- **Action:** Halt process and issue EXCEPTION with description.
- **Resolution:** Resume only when GA revises plan or HO provides new instructions.

---

## Structural Rules

Every exchange is prefixed with Handshake Turn Markers:

```
=== HANDSHAKE TURN N (agent) ===
/tag {agent}
```

These ensure deterministic sequencing and allow recovery if context is lost.

---

## Log Maintenance Rules

### Rule 1: Header Sections Are Live Status

Lanesborough Logs contain two types of content:

1. **Header sections** (Protocol Invocation, Role Assignments, Problem Statement) — These are **live status summaries** that reflect current state. They MUST be updated when log entries change protocol state.

2. **Log entries** — These are **append-only historical records**. Never edit past entries except for editorial notes flagged as `Type: housekeeping`.

### Rule 2: Human Gate Events Must Be Logged

When the Human Orchestrator (HO) grants approval, makes a decision, or otherwise advances the protocol past a gate, this MUST be recorded as a log entry:

```
### HO DECISION
**Timestamp:** [ISO 8601]
**Type:** gate-approval | decision | intervention | rejection
**Author:** [HO name]

[Description of what was approved/decided/rejected]

**Effect:** [What this enables - e.g., "Phase 1 may now proceed"]
```

### Rule 3: Editorial Notes Are Permitted

Non-substantive maintenance (fixing formatting, resolving merge conflicts, updating stale header status) may be recorded as editorial notes:

```
### EDITORIAL NOTE
**Timestamp:** [ISO 8601]
**Type:** housekeeping
**Author:** [Agent] with HO approval

[Description of what was fixed and why]
```

### Rule 4: Protocol Closure Requires Implementation Plan

When a Lanesborough Protocol debate concludes with HO approval, the closing agent MUST produce an **Implementation Plan** artifact.

---

## Gates

### Understanding Gate (UG)

"We are talking about the same thing, and I have responded to your verification flags."

The paraphrasing model must:
1. Restate the proposal in its own terms
2. Flag each claim with verification status: `[verified]`, `[contradicts: X]`, `[cannot verify: Y]`, `[unverifiable]`
3. NOT proceed without flagging—silence is not verification

The originating model must:
1. Confirm the paraphrase captures consequences, OR correct misunderstandings
2. Respond to each verification flag (defend, concede, or acknowledge uncertainty)

**UG closes when:**
- Model A has *responded* to all flags (not when all flags are green)
- Unverified claims are explicitly acknowledged with status, not papered over
- Human may certify unverifiable claims (after articulating them)

**UG does NOT close when:**
- Flags are ignored or hand-waved
- Model claims verification it didn't perform
- "I didn't check" is conflated with "I checked and it's fine"

### Agreement Gate (AG)

"We think the same thing is true/workable."

The reviewing model commits to a falsifiable, conditional, or explicitly unresolved stance. Agreement without demonstrated understanding is invalid.

**Critical distinction**: Understanding does NOT imply agreement. These are orthogonal.

### Articulation Gate (Human Qualification)

"I can restate this in my own words, so I understand what I'm approving."

The human must articulate:
- The core decision (before approving skill skeleton)
- Any claim they're certifying (before certification)
- What they're changing (before refining skill skeleton)

**Gate clears when:** Human restates the relevant assertion demonstrating comprehension.

**Gate fails when:** Human cannot articulate, or articulation reveals misunderstanding.

---

## Integration with Other Protocols

### Black Flag Protocol
- All agents follow epistemic hygiene rules.
- Claims must be cited rather than inferred.

### Temporal Validity Protocol
- Converged decisions become canonical documents.
- Supersession applies when specifications change.
