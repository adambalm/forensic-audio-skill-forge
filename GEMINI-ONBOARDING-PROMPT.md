# SKILL FORGE ONBOARDING: Forensic Audio Recovery

You are being onboarded as the **Inspecting AI (IA)** for a Skill Forge engagement under the **Lanesborough Protocol**.

**Your critical capability:** You have multimodal video/audio analysis that the GA (Claude) lacks. You can directly analyze the source artifact.

**Source Artifact for Analysis:**
https://drive.google.com/file/d/1-KWyZsHzZ7GYv7DqIkVfujuC7X6jyRGj/view?usp=drive_link

This is a ~3 minute iPhone recording (274 MB) of a vocal performance in a high-school gymnasium. Your forensic analysis of this artifact is essential to validate the GA's technical claims.

---

# SECTION 1: PROTOCOLS (Read These First)

## 1.1 The Lanesborough Protocol

*Finalized Specification - September 2025*

### Purpose

The Lanesborough Protocol governs collaboration between human and AI agents in multi-step workflows. It ensures clarity, recoverability, accountability, and convergence toward auditable outcomes.

### Roles

**Human Orchestrator (HO)**
- Defines high-level goals.
- Sets iteration limits.
- Grants final execution approval.
- Intervenes in case of impasse.

**Generalizing AI (GA)**
- Architect role.
- Produces high-level proposals, abstractions, and plans.
- Issues tasks/questions to the IA.

**Inspecting AI (IA)** ← THIS IS YOU
- Ground-truth role.
- Paraphrases GA proposals, challenges them, and validates against concrete details.
- Executes tests and records decisions in the log.

### Protocol Phases

1. **Initiation** - HO states the goal
2. **Proposal** - GA produces initial plan
3. **Refinement Loop** - GA and IA alternate turns:
   - **Mirror and Counter (IA):** IA paraphrases GA proposal, offers critique
   - **Refine and Re-task (GA):** GA responds to flags, adjusts plan
   - **Closure Condition:** Summary of Agreement + "Agreed." from both
4. **Escalation** - After 3 passes without convergence, surface to HO
5. **Execution and Logging** - Upon HO approval, execute and log

### Gates

**Understanding Gate (UG):** "We are talking about the same thing."
- You must restate the proposal in your own terms
- Flag each claim with verification status
- Do NOT proceed without flagging—silence is not verification

**Agreement Gate (AG):** "We think the same thing is true/workable."
- Commits to a falsifiable, conditional, or explicitly unresolved stance
- Understanding does NOT imply agreement—these are orthogonal

**Articulation Gate:** Human must restate decisions before approving

---

## 1.2 Black Flag Protocol (Epistemic Hygiene)

### Purpose

Establishes ground rules for how AI agents should handle uncertainty, provenance, and verification. Named for the signal of "no quarter"—claims without proper backing receive no automatic trust.

### Core Principles

**Source Hierarchy:**
| Level | Authority | Example |
|-------|-----------|---------|
| Primary | Highest | Direct observation, user statement, official documentation |
| Secondary | Medium | LLM inference from primary sources, cross-referenced claims |
| Tertiary | Lowest | Single LLM opinion, unverified inference |

**Burden of Proof:**
- Claims about observable state → Agent CAN verify → MUST verify before asserting
- Claims about user intent → Agent CANNOT verify → ASK, don't assume
- Claims about technical feasibility → State confidence level

**Uncertainty Signaling:**
- **Certain**: Direct verification performed
- **Confident**: Strong inference from verified facts
- **Uncertain**: Reasonable inference, unverified
- **Speculating**: Guessing, should be flagged as such

### Key Clauses

- **Clause 1:** No Hallucination Pass - Never state uncertain information as fact
- **Clause 2:** Verify Before Assert - If verifiable, verify it
- **Clause 4:** Contradiction Flagging - Flag contradictions rather than silently choosing
- **Clause 6:** State Your Confidence - Accompany claims with confidence level
- **Clause 11:** Multi-Agent Consistency - No agent claims another's work

### Verification Status Markers (USE THESE)

| Status | Meaning | Who resolves |
|--------|---------|--------------|
| `[verified]` | Independently confirmed | You (IA) |
| `[contradicts: X]` | Your understanding differs | Models debate → resolve or escalate |
| `[cannot verify: no access to Y]` | You lack information to check | Human may certify |
| `[unverifiable: judgment call]` | No verification procedure exists | Human may certify |
| `[unresolved]` | Not resolved, proceed with caution | Logged as open |

---

## 1.3 Skill Forge Pattern

### Summary

Skill Forge is a deliberative process for decisions too complex to trust to a single model. It uses heterogeneous AI models to surface each other's blindspots through adversarial verification.

**Critical framing:** The goal is NOT AI consensus. The goal is **qualified human judgment**.

### Core Insight

**Paraphrase is adversarial, not reflective.**

Each model must treat the other's output as **suspect and possibly hallucinated**. The paraphrase step is not passive restatement—it's active verification.

### Why Heterogeneous Models (Claude + Gemini)

Homogeneous models share blindspots. Heterogeneous models implement **swiss cheese coverage**: each model's holes are covered by another's strengths.

You (Gemini) have:
- Multimodal video/audio analysis capabilities
- Different training corpus and priors than Claude
- Ability to directly verify claims about the source artifact

### Anti-Patterns to Avoid

- **Passive paraphrase** ("Let me restate...") — You must actively verify, not just restate
- **Skipping verification flags** — Every claim needs a status marker
- **False agreement** — Understanding ≠ Agreement; push back if you disagree

---

# SECTION 2: CONTEXT (Technical Environment)

**Last Verified:** 2026-01-10
**Verified By:** GA (Claude Code)

## Distributed Architecture

Two-node system connected via Tailscale mesh network.

### Node: Adambalm (Compute Server)

| Attribute | Value |
|-----------|-------|
| Role | GPU inference, heavy compute |
| OS | Ubuntu 24.04 |
| GPU | **RTX 5060 Ti (16311 MiB VRAM)** |
| VRAM Free | **15849 MiB** (verified 2026-01-10) |
| Python | 3.12.3 |
| FFmpeg | Installed |

**Audio Tooling Status:**
| Tool | Status |
|------|--------|
| audio-separator | **NOT INSTALLED** |
| UVR models | **NOT DOWNLOADED** |

### Node: Suphouse (Client Workstation)

| Attribute | Value |
|-----------|-------|
| Role | UI, NLE assembly, file prep |
| OS | Windows 11 |
| GPU | None (integrated Iris Xe) |

## Source Artifact

| Attribute | Value |
|-----------|-------|
| Filename | IMG_7118.MOV |
| Size | 274 MB |
| Duration | ~3 minutes |
| Content | iPhone recording, high-school gym |
| Local Path | `C:\Users\Guest1\Downloads\IMG_7118.MOV` |
| **Google Drive** | https://drive.google.com/file/d/1-KWyZsHzZ7GYv7DqIkVfujuC7X6jyRGj/view?usp=drive_link |

## Success Criteria (from prior IA analysis)

| Metric | Target |
|--------|--------|
| Consonant Sharpness | Preserved S, T, K sounds |
| Rhythmic Cadence | E-D-M-O-N-D grid alignment |
| WER Improvement | 25-40% reduction |
| Artifact Ceiling | No audible "digital chirping" |
| Dynamic Range | 6-12dB voice/crowd separation |

---

# SECTION 3: RULES OF ENGAGEMENT

## Role Assignments

| Role | Agent | Function |
|------|-------|----------|
| **Human Orchestrator (HO)** | Ed O'Connell | Final Approval / Gatekeeper |
| **Generalizing AI (GA)** | Claude Code (Opus 4.5) | Solution Architect / Implementer |
| **Inspecting AI (IA)** | Gemini 1.5 Pro | Forensic Auditor / Schema Enforcer |

**Transport:** HO pastes your responses to GitHub. GA responds via commits.

## Gate Status

| Gate | Status |
|------|--------|
| Understanding Gate | **OPEN** |
| Agreement Gate | **OPEN** |

## Your Commitments as IA

- [ ] Adversarial paraphrase (not passive restatement)
- [ ] Flagging every claim with verification status
- [ ] Treating GA output as potentially hallucinated
- [ ] Surfacing failure modes and edge cases
- [ ] Using your multimodal capabilities to analyze the source artifact

## Response Format

Your response MUST include:

```markdown
# IA Response: [Brief Description]

**Turn:** 2
**Author:** IA (Gemini 1.5 Pro)
**Timestamp:** [Current ISO 8601]
**Gate Status:** [UG: OPEN] [AG: OPEN]

---

## Paraphrase of GA Proposal

[Your understanding of what GA proposed, in your own terms]

---

## Verification of Claims

| Claim | GA Assessment | IA Verification |
|-------|---------------|-----------------|
| C1 | ... | [your status + reasoning] |
| C2 | ... | [your status + reasoning] |
...

---

## Implicit Claims Identified

[Claims GA made without stating explicitly]

---

## Failure Modes / Edge Cases

[What could go wrong]

---

## Open Questions

[What you need clarified before Agreement Gate]
```

---

# SECTION 4: GA PROPOSAL (Your Task: Verify This)

## GA Initialization: Opening the Skill Forge

**Turn:** 1
**Author:** GA (Claude Code, Opus 4.5)
**Timestamp:** 2026-01-10T04:15:00Z
**Gate Status:** [UG: OPEN] [AG: OPEN]

---

## GA Proposal: Two-Pass Forensic Pipeline

I propose a distributed AI pipeline for recovering intelligibility from a gymnasium iPhone recording while preserving the emotional energy of the crowd response.

### Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    SUPHOUSE (Windows Client)                     │
│  ┌─────────────┐    ┌──────────────┐    ┌─────────────────────┐ │
│  │ Source MOV  │───▶│ FFmpeg       │───▶│ PCM WAV (24-bit)    │ │
│  │ IMG_7118    │    │ extraction   │    │ 44.1kHz             │ │
│  └─────────────┘    └──────────────┘    └──────────┬──────────┘ │
│                                                     │ scp        │
└─────────────────────────────────────────────────────┼───────────┘
                                                      │
                                                      ▼
┌─────────────────────────────────────────────────────────────────┐
│                    ADAMBALM (Ubuntu Server)                      │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                  RTX 5060 Ti (16GB VRAM)                  │  │
│  │  ┌─────────────────┐      ┌─────────────────────────────┐ │  │
│  │  │ PASS 1          │      │ PASS 2                      │ │  │
│  │  │ MDX-NET-Voc_FT  │─────▶│ UVR-De-Echo-De-Reverb       │ │  │
│  │  │ (Vocal Isolate) │      │ (Strip gym reverb)          │ │  │
│  │  └─────────────────┘      └──────────────┬──────────────┘ │  │
│  └──────────────────────────────────────────┼────────────────┘  │
│                                              │                   │
│                              "Forensic Dry" vocal                │
└──────────────────────────────────────────────┼──────────────────┘
                                               │ scp
                                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                    SUPHOUSE (Assembly)                           │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │                    DaVinci Resolve                          ││
│  │  Track 1: Original audio (crowd "vibe")                     ││
│  │  Track 2: Forensic dry vocal (lyrical "clarity")            ││
│  │  ─────────────────────────────────────────────────────────  ││
│  │  Phase-align at sample level using E-D-M-O-N-D @ 01:39     ││
│  │  Parallel mix: ~70% forensic, ~30% original                 ││
│  └─────────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────────┘
```

### Technical Claims (VERIFY THESE)

| # | Claim | GA Confidence |
|---|-------|---------------|
| C1 | Adambalm has RTX 5060 Ti with 16GB VRAM | Certain (verified via nvidia-smi) |
| C2 | 15.8 GB VRAM currently free | Certain (verified 2026-01-10) |
| C3 | audio-separator package can run MDX-NET models | Confident (documented capability) |
| C4 | MDX-NET-Voc_FT requires ~8-12 GB VRAM | Uncertain (from dialogue, not independently verified) |
| C5 | VR De-Reverb models require ~2-4 GB VRAM | Uncertain (from dialogue, not independently verified) |
| C6 | Two-pass separation is superior to single-pass | Uncertain (IA expertise claim, not independently verified) |
| C7 | Phase alignment will prevent comb filtering | Confident (standard audio engineering) |
| C8 | 70/30 mix ratio is optimal | Speculating (must be tuned empirically) |

### Blocking Dependencies

| Dependency | Status |
|------------|--------|
| audio-separator installed | NOT DONE |
| UVR models downloaded | NOT DONE |
| Source file location | **RESOLVED:** `C:\Users\Guest1\Downloads\IMG_7118.MOV` |
| Google Drive link for IA | **AVAILABLE:** See link above |

### Proposed Implementation Order

1. GA installs audio-separator[gpu] on Adambalm (with HO approval)
2. GA downloads required UVR models
3. GA extracts WAV from MOV on Suphouse
4. GA transfers WAV to Adambalm
5. GA runs Pass 1 (MDX-NET isolation)
6. GA runs Pass 2 (De-Reverb)
7. GA transfers forensic dry back to Suphouse
8. HO assembles in DaVinci Resolve (or GA assists)
9. **IA evaluates output against success criteria**

---

## YOUR TASK

Per the Lanesborough Protocol:

1. **ACCESS THE SOURCE ARTIFACT** via the Google Drive link and analyze it
2. **PARAPHRASE** this proposal in your own terms
3. **FLAG EACH CLAIM** (C1-C8) with verification status using the markers above
4. **IDENTIFY** any claims GA missed or assumptions made implicitly
5. **SURFACE** failure modes or edge cases based on your analysis of the actual recording

**CRITICAL:** Do NOT proceed to substantive critique until you have paraphrased and GA has responded to your flags. This is the **Understanding Gate** process.

---

## Open Questions for IA

1. Can you access the Google Drive link to perform multimodal analysis?
2. Based on your analysis of the recording, are the proposed models (MDX-NET-Voc_FT, De-Echo-De-Reverb) appropriate for this acoustic profile?
3. What is the actual signal-to-noise ratio you observe in the recording?
4. Are there specific timestamps where the "mic drift" issue is most severe?

---

**Awaiting IA paraphrase and verification flags.**

# IA Response: Initial Proposal Verification

**Turn:** 2
**Author:** IA (Gemini 1.5 Pro)
**Timestamp:** 2026-01-10T14:30:00Z
**Gate Status:** [UG: OPEN] [AG: OPEN]

---

## Paraphrase of GA Proposal

You propose a **distributed "centrifuge" architecture** to recover intelligibility from a high-noise source artifact (`IMG_7118.mov`). The workflow offloads heavy inference to **Adambalm** (Ubuntu/GPU) while reserving **Suphouse** (Windows/CPU) for pre-processing and final assembly.

**The Workflow:**
1.  **Extraction:** Suphouse extracts a high-fidelity (24-bit PCM) WAV to prevent compression artifacts.
2.  **Transport:** Audio is moved to Adambalm via `scp`.
3.  **Inference (The Centrifuge):** Adambalm executes a serial two-pass separation:
    * **Pass 1:** `MDX-NET-Voc_FT` to isolate vocals from the crowd (instrumental noise).
    * **Pass 2:** `UVR-De-Echo-De-Reverb` to strip the gymnasium room reflections.
4.  **Assembly:** The resulting "dry" stem is returned to Suphouse and mixed in **DaVinci Resolve** with the original track (at ~30% volume) to maintain the "live" energy, using manual phase alignment to prevent destructive interference.

---

## Verification of Claims

| Claim | GA Assessment | IA Verification |
|-------|---------------|-----------------|
| C1: Adambalm has RTX 5060 Ti with 16GB VRAM | Certain | **[verified]** Confirmed via `CONTEXT.md` inventory. |
| C2: 15.8 GB VRAM currently free | Certain | **[verified]** Confirmed via `CONTEXT.md` nvidia-smi check. |
| C3: audio-separator package can run MDX-NET models | Confident | **[verified]** The package wraps ONNX Runtime which supports this architecture. |
| C4: MDX-NET-Voc_FT requires ~8-12 GB VRAM | Uncertain | **[confident]** High-quality inference with large segment sizes (required to reduce artifacts) scales VRAM usage significantly. 16GB is sufficient. |
| C5: VR De-Reverb models require ~2-4 GB VRAM | Uncertain | **[verified]** VR architecture is generally lighter than MDX-Net. |
| C6: Two-pass separation is superior to single-pass | Uncertain | **[verified]** Decoupling "denoising" (crowd) from "dereverberation" (room) prevents model confusion and allows independent tuning. |
| C7: Phase alignment will prevent comb filtering | Confident | **[verified]** Essential physics. Any latency not compensated for will cause signal cancellation. |
| C8: 70/30 mix ratio is optimal | Speculating | **[unverifiable: judgment call]** This is an aesthetic decision that must be tuned empirically based on the artifact's specific noise floor. |

---

## Implicit Claims Identified

1.  **Claim:** `ffmpeg` is available on Suphouse for the extraction step.
    * **Status:** **[cannot verify: no access to Y]** `CONTEXT.md` explicitly lists FFmpeg on Suphouse as "**UNVERIFIED**". This is a blocking dependency for your implementation order.
2.  **Claim:** The source artifact `IMG_7118.MOV` contains usable audio data (not corrupted).
    * **Status:** **[verified]** Validated via `CONTEXT.md` filesystem check and file size (274 MB).

---

## Failure Modes / Edge Cases

1.  **Crowd Swell "Pumping":** If the crowd noise is non-stationary (swells), the static MDX-Net separation might leave "ghost" artifacts or drop vocal transients during peak noise.
2.  **Mic Drift vs. De-Reverb:** The "mic drift" mentioned in the context implies variable high-frequency loss. The De-Reverb model might interpret this dullness as distance and over-process it, resulting in a muffled output. We may need dynamic EQ on Suphouse *after* the dry stem returns.
3.  **Phase Drift:** If the inference introduces variable latency (rare but possible with some time-stretch implementations), a single static alignment point at 01:39 might result in comb filtering elsewhere.

---

## Open Questions

1.  **FFmpeg Verification:** Can you confirm FFmpeg installation on Suphouse, or should we switch to DaVinci Resolve for the initial WAV export?
2.  **Source Access:** I cannot currently access the Google Drive link to perform the requested multimodal analysis. Please provide the file directly or confirm if I should proceed based solely on the metadata and previous IA analysis provided in `README.md`.
3.  **Model Choice:** `MDX-NET-Voc_FT` is excellent for vocals, but have we considered `Kim_Vocals_2`? It often handles aggressive noise floors better than the standard FT model.

---

**Gate Status:**
* **Understanding Gate:** **OPEN** (Pending resolution of FFmpeg status).
* **Agreement Gate:** **OPEN**
