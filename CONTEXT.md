# Context: Environment and Technical Constraints

**Last Verified:** 2026-01-10T04:10:00Z
**Verified By:** GA (Claude Code)

---

## Distributed Architecture

This engagement uses a two-node distributed architecture connected via Tailscale mesh network.

### Node: Adambalm (Compute Server)

| Attribute | Value | Verification |
|-----------|-------|--------------|
| Role | GPU inference, heavy compute | [verified] |
| OS | Ubuntu 24.04 | [verified: Environment Inventory] |
| CPU | i5-11400 @ 2.6GHz | [verified: Environment Inventory] |
| RAM | 64 GB (41 GB available) | [verified: Environment Inventory] |
| GPU | **RTX 5060 Ti (16311 MiB VRAM)** | [verified: nvidia-smi 2026-01-10] |
| VRAM Free | **15849 MiB** | [verified: nvidia-smi 2026-01-10] |
| Tailscale IP | 100.111.114.84 | [verified: Environment Inventory] |
| Python | 3.12.3 | [verified: ssh check 2026-01-10] |
| FFmpeg | Installed at /usr/bin/ffmpeg | [verified: ssh check 2026-01-10] |
| Docker | 28.5.1 | [verified: Environment Inventory] |

**Audio Tooling Status:**
| Tool | Status | Notes |
|------|--------|-------|
| audio-separator | **NOT INSTALLED** | [verified: pip list 2026-01-10] |
| UVR models | **NOT DOWNLOADED** | Requires audio-separator first |
| forensic-audio directory | **DOES NOT EXIST** | [verified: test -d 2026-01-10] |

### Node: Suphouse (Client Workstation)

| Attribute | Value | Verification |
|-----------|-------|--------------|
| Role | UI, NLE assembly, file prep | [verified] |
| OS | Windows 11 | [verified: Environment Inventory] |
| CPU | i7-1255U (12th gen) | [verified: Environment Inventory] |
| RAM | 16 GB | [verified: Environment Inventory] |
| GPU | None (integrated Iris Xe) | [verified: Environment Inventory] |
| Tailscale IP | 100.126.163.59 | [verified: Environment Inventory] |
| Node.js | v20.18.1 | [verified: Environment Inventory] |
| Python | 3.12.10 | [verified: Environment Inventory] |
| FFmpeg | **UNVERIFIED** | Not in Environment Inventory |

### Network Connectivity

| Path | Method | Status |
|------|--------|--------|
| Suphouse → Adambalm | `ssh adambalm` (key auth) | [verified: working] |
| File transfer | `scp` via Tailscale | [verified: Environment Inventory] |

---

## Constraints

| Constraint | Impact | Mitigation |
|------------|--------|------------|
| No GPU on Suphouse | Cannot run local inference | Offload to Adambalm |
| 16GB VRAM limit on Adambalm | Large models spill to RAM | Use MDX-Net (8-12GB), not mega models |
| Audio-separator not installed | Cannot run inference yet | **BLOCKING: Must install first** |
| Single GPU | ComfyUI blocks during generation | Ensure ComfyUI idle during audio work |

---

## Source Artifact

| Attribute | Value | Status |
|-----------|-------|--------|
| Filename | IMG_7118.mov | [cannot verify: location unknown] |
| Format | QuickTime MOV | [verified: dialogue transcript] |
| Duration | ~3 minutes | [verified: dialogue transcript] |
| Content | iPhone recording, high-school gym | [verified: dialogue transcript] |
| Location | **UNKNOWN** | HO must specify path |

---

## Technical Pipeline (Proposed)

```
Phase 1: Environment Setup (Adambalm)
├── Create ~/forensic-audio directory
├── Create Python venv
├── Install audio-separator[gpu]
├── Download UVR models (MDX-NET-Voc_FT, De-Echo-De-Reverb)
└── Verify VRAM usage

Phase 2: Source Acquisition (Suphouse → Adambalm)
├── Locate IMG_7118.mov on Suphouse
├── Extract audio: ffmpeg -i IMG_7118.mov -vn -acodec pcm_s24le -ar 44100 source.wav
├── Transfer: scp source.wav adambalm:~/forensic-audio/
└── Verify file integrity (hash check)

Phase 3: Centrifuge Inference (Adambalm)
├── Pass 1: audio-separator source.wav --model UVR-MDX-NET-Voc_FT --output_dir ./pass1
├── Pass 2: audio-separator ./pass1/Vocals_source.wav --model UVR-De-Echo-De-Reverb --output_dir ./final
└── Transfer results back to Suphouse

Phase 4: Assembly (Suphouse)
├── Import original video + forensic dry vocal to DaVinci Resolve
├── Phase-align at sample level (use E-D-M-O-N-D @ 01:39 as sync point)
├── Parallel mix: original for "vibe", forensic for "clarity"
└── Export final artifact
```

---

## Blocking Items

Before proceeding with implementation, these must be resolved:

1. **[BLOCKING] audio-separator installation** - Requires HO approval to install on Adambalm
2. **[BLOCKING] Source artifact location** - HO must specify path to IMG_7118.mov
3. **[OPTIONAL] FFmpeg on Suphouse** - Verify availability or install

---

## MCP/API Availability

| Tool | Availability | Notes |
|------|--------------|-------|
| DaVinci Resolve MCP | [unverified] | Mentioned in dialogue, not confirmed |
| Stem Generation MCP | [unverified] | Mentioned in dialogue, not confirmed |
| audio-separator CLI | Available via pip | Standard CLI, no MCP wrapper |

---

## Success Criteria

From IA analysis in dialogue:

| Metric | Target | Measurement |
|--------|--------|-------------|
| Consonant Sharpness | Preserved S, T, K sounds | Spectrogram analysis > 6kHz |
| Rhythmic Cadence | E-D-M-O-N-D grid alignment | Manual verification at 01:39 |
| WER Improvement | 25-40% reduction | Transcription comparison |
| Artifact Ceiling | No audible "digital chirping" | Listening test on silent gaps |
| Dynamic Range | 6-12dB voice/crowd separation | RMS metering |
