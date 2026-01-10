# Forensic Audio Skill Forge

**Pattern:** MDX-Net/VR Centrifuge
**Status:** Understanding Gate OPEN
**Date Initiated:** 2026-01-10

---

## Purpose

This repository serves as the deliberation medium for a **Skill Forge** engagement under the **Lanesborough Protocol**. The goal is to extract a reusable **Thin Skill** for forensic audio recovery of high-density creative performances captured in adverse acoustic environments.

## Engagement Context

A technically precise vocal performance (Rakim-style meter, ~95 BPM) was recorded on an iPhone in a high-school gymnasium. The recording suffers from:
- Extreme room reverb ("gym bloom")
- Non-stationary crowd noise
- Mic drift causing high-frequency transient loss

The objective is to recover intelligibility while preserving the emotional "vibe" of the live event.

## Technical Approach

**Distributed AI Pipeline:**
- **Adambalm** (RTX 5060 Ti, 16GB VRAM): GPU-accelerated vocal isolation and de-reverb using MDX-Net and VR architectures
- **Suphouse** (i7-1255U, 16GB RAM): Lossless extraction, parallel mixing in DaVinci Resolve

## Role Assignments

| Role | Agent | Function |
|------|-------|----------|
| **Human Orchestrator (HO)** | Ed O'Connell | Final Approval / Gatekeeper |
| **Generalizing AI (GA)** | Claude Code (Opus 4.5) | Solution Architect / Implementer |
| **Inspecting AI (IA)** | Gemini 1.5 Pro | Forensic Auditor / Schema Enforcer |

**Transport:** GitHub commits and markdown files

## Gate Status

| Gate | Status |
|------|--------|
| Understanding Gate | **OPEN** |
| Agreement Gate | **OPEN** |

## Repository Structure

```
forensic-audio-skill-forge/
├── README.md                      # This file
├── RULES-OF-ENGAGEMENT.md         # Full protocol specifications
├── CONTEXT.md                     # Environment inventory and constraints
├── protocols/                     # Individual protocol documents
│   ├── black-flag-protocol.md
│   ├── lanesborough-protocol.md
│   ├── skill-forge-pattern.md
│   └── temporal-validity-protocol.md
├── dialogue/                      # Deliberation exchanges
│   └── 001-initialization.md      # Opening prompt for IA
└── artifacts/                     # Technical outputs
```

## How to Participate

### For IA (Gemini)
1. Read `RULES-OF-ENGAGEMENT.md` to understand the protocol constraints
2. Read `CONTEXT.md` for the technical environment
3. Begin with `dialogue/001-initialization.md`
4. Respond by creating `dialogue/002-ia-response.md` (or HO will paste your response)

### For GA (Claude Code)
1. Monitor dialogue files for IA responses
2. Respond in sequence (003, 004, etc.)
3. Track gate status in this README

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
