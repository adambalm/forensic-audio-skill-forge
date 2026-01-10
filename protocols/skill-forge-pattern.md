# Skill Forge Pattern

## Summary

Skill Forge is a deliberative process for decisions too complex to trust to a single model or a single human judgment. It uses heterogeneous AI models to surface each other's blindspots through adversarial verification, then requires the human to demonstrate understanding before approving a model-produced skill. Full deliberation is expensive; the cost is amortized when the result is captured as an invocable skill for future decisions.

**Critical framing:** The goal is NOT AI consensus. The goal is **qualified human judgment**. The model produces the skill skeleton; the human's articulation proves they're qualified to approve it.

## When to Use

*Problem signature that triggers this pattern:*

- You face a **novel problem** requiring judgment beyond routine application of existing knowledge
- The problem domain is **technically complex** such that a single model (or single human) may have blindspots
- You need the human decision-maker to be **genuinely qualified**, not rubber-stamping
- The class of problem is **likely to recur**, making the upfront deliberation cost worthwhile
- You want to **accumulate executive capacity** over time, not just make isolated decisions

## Core Insight

The goal is not AI consensus or automated recommendation. The goal is **qualified human judgment** — expanding what complexity a human can competently decide by observing models surface each other's errors through adversarial verification.

**Paraphrase is adversarial, not reflective:**

Each model must treat the other's output as **suspect and possibly hallucinated**. The paraphrase step is not passive restatement—it's active verification.

| Layer | Function |
|-------|----------|
| Model B paraphrases Model A's proposal | Restates AND flags each claim with verification status |
| Model A paraphrases Model B's critique | Restates AND flags each claim with verification status |
| **Human articulates the outcome** | **Qualification gate** — if the human cannot restate the core, they cannot approve |

**Verification status per claim:**

| Status | Meaning | Who resolves |
|--------|---------|--------------|
| `[verified]` | Model B independently confirmed | Model B |
| `[contradicts: X]` | Model B's understanding differs | Models debate → resolve or escalate |
| `[cannot verify: no access to Y]` | Model B lacks information to check | Human may certify (after articulating the claim) |
| `[unverifiable: judgment call]` | No verification procedure exists | Human may certify (after articulating the claim) |
| `[unresolved]` | Not resolved, proceed with caution | Logged as open |

**Human certification:**

When models cannot verify a claim (lack of access, judgment call), the Human Orchestrator may certify it: `[certified by HO, YYYY-MM-DD]`. But certification is also gated: the human must first articulate the claim they're certifying. This:
- Breaks deadlocks without forcing false consensus
- Puts the human's name on the claim, not "the models agreed"
- Prevents certifying claims the human doesn't actually understand
- Enables targeted re-forge when certified claims later prove wrong

**The forge metaphor:**
- Deliberation is the forge (expensive, high-heat)
- Human articulation is the gate (proves qualification)
- Model-produced skill is the output (human approves after qualifying)
- Reuse amortizes cost across future decisions

## Mechanism

### 1. Novel Problem Triggers Full Deliberation

When existing skills don't apply or fail, invoke the full protocol:

1. **Human initiates** → prompts Model A for proposal
2. **Paraphrase-verify cycle** → Model B paraphrases AND flags each claim with verification status
3. **Understanding Gate (UG)** → closes when Model A has responded to all flags (not when all green)
4. **Substantive critique** → Model B surfaces failure modes, proposes tests (only after UG closed)
5. **Paraphrase reverses** → Model A paraphrases critique with flags, Model B confirms
6. **Agreement Gate (AG)** → executable test or qualified agreement
7. **Escalation** → after 3 passes without convergence, surface open questions to human
8. **Skill skeleton** → model(s) produce skill structure capturing the decision

### 2. Human Articulation Gate

The human, having observed the exchange, must restate the core decision in their own words. This is a **gate**, not a production step:

> If the Human Orchestrator cannot articulate the core decision in their own words, they cannot approve or refine the skill skeleton. The protocol has failed.

**Articulation proves qualification.** The human who can articulate it understands what they're approving. The human who cannot articulate it is rubber-stamping.

### 3. Human Approves Skill

After passing the articulation gate, the human may:
- **Approve** the model-produced skeleton as-is
- **Refine** specific parts (but must articulate what they're changing)

The approved skill is now authorized for use with full provenance:
- **Invocable**: Can be triggered when similar problems arise
- **Parameterizable**: Generalizes beyond the single case
- **Provenance-scored**: Per-claim verification status, who certified what, what the human articulated

### 4. Similar Problem → Invoke Skill

Next time this problem class arises, invoke the skill instead of re-running full deliberation. The expensive upfront cost is amortized.

### 5. Skill Fails → Route Back to Forge

When the skill fails to apply or produces unsatisfactory results, the failure routes back into full deliberation. New deliberation produces new skill skeleton; human must re-qualify (articulate) to approve.

## Why Heterogeneous Models

Homogeneous models (same architecture, same training data) tend to share blindspots. Heterogeneous models—with genuinely different training corpora, optimization targets, and priors—implement **swiss cheese coverage**: each model's holes are covered by another's strengths.

The paraphrase step is where this coverage manifests. When Model B paraphrases Model A's proposal, it translates through its own priors:
- Emphasizes different aspects
- Interprets ambiguous terms differently
- Flags claims it cannot verify
- Surfaces assumptions Model A didn't know it was making

This is why the pattern uses different LLM providers (e.g., Claude + Gemini), not just different instances of the same model.

## What Accumulates

| What | How |
|------|-----|
| **Human qualification** | They passed the articulation gate — demonstrated understanding of what they approved |
| **System capability** | Skill is invocable — cheaper than re-deliberation |
| **Domain coverage** | More skills = more solved problem classes |
| **Efficiency** | Full deliberation only for genuinely novel problems |
| **Provenance** | Per-claim verification status, who certified what, what they articulated |
| **Failure targeting** | When skill fails, trace to which claim broke and who certified it |

## Anti-Patterns

- **Using for trivial decisions** — overhead exceeds value; invoke existing skills instead
- **Skipping human articulation** — rubber-stamping; no demonstrated understanding; accountability is hollow
- **Human writes the skill** — bypasses model's ability to capture deliberation structure; loses provenance
- **Human approves without articulating** — same as skipping; must demonstrate understanding first
- **Human refines without articulating what** — editing something you don't understand introduces errors
- **Human certifies without articulating the claim** — certifying something you can't restate means you don't know what you're certifying
- **Homogeneous models** — shared blindspots defeat the purpose
- **Not capturing the skill** — deliberation cost is wasted if not amortized
- **Routing around failures** — skill failures must return to the forge, not be patched ad-hoc
- **Passive paraphrase** ("Let me restate...") — relies on emergent self-correction; no verification performed
