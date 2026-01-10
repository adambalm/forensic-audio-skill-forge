# Forensic Audio Skill Forge

**Pattern:** MDX-Net/VR Centrifuge
**Status:** Understanding Gate APPROACHING CLOSURE
**Date Initiated:** 2026-01-10

---

## Purpose

This repository serves as the deliberation medium for a **Skill Forge** engagement under the **Lanesborough Protocol**. The goal is to extract a reusable **Thin Skill** for forensic audio recovery of high-density creative performances captured in adverse acoustic environments.

## Canonical Dialogue

**ALL DIALOGUE HAPPENS IN ONE FILE:**

### [`LANESBOROUGH-LOG.md`](LANESBOROUGH-LOG.md)

This is the single source of truth. It contains:
- Protocol rules (so IA doesn't need external references)
- Problem statement and context
- All dialogue turns (append-only)
- Gate status (live header)

**DO NOT create separate dialogue files.** Append your turns to LANESBOROUGH-LOG.md.

---

## Engagement Context

A technically precise vocal performance (Rakim-style meter, ~95 BPM) was recorded on an iPhone in a high-school gymnasium. The recording suffers from:
- Extreme room reverb ("gym bloom")
- Non-stationary crowd noise
- Mic drift causing high-frequency transient loss

The objective is to recover intelligibility while preserving the emotional "vibe" of the live event.

## Role Assignments

| Role | Agent | Function |
|------|-------|----------|
| **Human Orchestrator (HO)** | Ed O'Connell | Final Approval / Gatekeeper |
| **Generalizing AI (GA)** | Claude Code (Opus 4.5) | Solution Architect / Implementer |
| **Inspecting AI (IA)** | Gemini 1.5 Pro | Forensic Auditor / Schema Enforcer |

**Transport:** HO pastes IA responses to GitHub. GA responds via commits.

## Gate Status

| Gate | Status |
|------|--------|
| Understanding Gate | **APPROACHING CLOSURE** |
| Agreement Gate | **OPEN** |

## Repository Structure

```
forensic-audio-skill-forge/
├── README.md                      # This file
├── LANESBOROUGH-LOG.md            # ★ CANONICAL DIALOGUE - all turns here
├── CONTEXT.md                     # Environment inventory (reference)
├── RULES-OF-ENGAGEMENT.md         # Full protocol specs (reference)
├── protocols/                     # Individual protocol documents (reference)
│   ├── black-flag-protocol.md
│   ├── lanesborough-protocol.md
│   ├── skill-forge-pattern.md
│   └── temporal-validity-protocol.md
└── artifacts/                     # Technical outputs (when produced)
```

## How to Participate

### For IA (Gemini)
1. **Read ONLY [`LANESBOROUGH-LOG.md`](LANESBOROUGH-LOG.md)** - it contains everything you need
2. Append your response to that file following the format shown
3. HO will paste your response or you commit directly

### For GA (Claude Code)
1. Monitor LANESBOROUGH-LOG.md for IA responses
2. Append responses to the same file
3. Update gate status in header when appropriate

### For HO (Ed)
1. Approve gate closures
2. Certify unverifiable claims when appropriate
3. Intervene on impasse

## Success Criteria

From IA's initial analysis:
- **Consonant Sharpness preservation** (S, T, K sounds in "tracks", "practice")
- **Rhythmic Cadence preservation** (the E-D-M-O-N-D grid alignment)
- **25-40% WER improvement** while maintaining crowd energy

---

*This engagement is governed by the Lanesborough Protocol. All participants commit to Black Flag epistemic hygiene.*
